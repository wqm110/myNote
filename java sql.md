# java sql  
```java
package com.ruoyi.project.oa.financereceivableinfo.mapper.sqlprovider;

import com.ruoyi.common.utils.sql.SqlUtil;
import com.ruoyi.project.oa.financereceivableinfo.domain.OaPurchaseApply;
import com.ruoyi.project.oa.financereceivableinfo.domain.OaPurchaseApplyDto;
import org.apache.commons.lang3.ArrayUtils;
import org.apache.ibatis.annotations.Param;
import org.apache.ibatis.jdbc.SQL;
import org.springframework.util.StringUtils;

import java.util.Date;

/**
 * @author pengcheng
 */
public class OaPurchaseApplySqlProvider {

    public String selectSingleOaPurchaseApply(String applyProductId) {
        SQL sql = new SQL() {

            private final String[] FIELDS = new String[]{
                    "oa_purchase_apply.apply_product_id",
                    "oa_purchase_apply.apply_user_id",
                    "oa_purchase_apply.apply_dept",
                    "oa_purchase_apply.apply_time",
                    "oa_purchase_apply.total_amount",
                    "oa_purchase_apply.reason_for_purchase",
                    "oa_purchase_apply.status",
                    "oa_purchase_apply.remark"
            };

            {
                SELECT(FIELDS);
                FROM("oa_purchase_apply");
                //构建条件子句
                WHERE("oa_purchase_apply.apply_product_id = #{applyProductId}");
            }
        };
        String sqlStr = sql.toString();
        return sqlStr;
    }

    public String selectOaPurchaseApplyWithDetail(String applyProductId) {
        SQL sql = new SQL() {

            private final String[] FIELDS = new String[]{
                    "oa_dev.oa_purchase_apply.apply_product_id",
                    "oa_dev.oa_purchase_apply.apply_user_id",
                    "oa_dev.sys_user.nick_name AS apply_user_name",
                    "oa_dev.oa_purchase_apply.apply_dept",
                    "oa_dev.sys_dept.dept_name AS apply_dept_name",
                    "oa_dev.oa_purchase_apply.apply_time",
                    "oa_dev.oa_purchase_apply.total_amount",
                    "oa_dev.oa_purchase_apply.reason_for_purchase",
                    "oa_dev.oa_purchase_apply.status",
                    "oa_dev.oa_purchase_apply.remark",
                    "oa_dev.oa_purchase_detail_product.product_id",
                    "oa_dev.oa_purchase_detail_product.apply_product_id",
                    "oa_dev.oa_purchase_detail_product.product_name",
                    "oa_dev.oa_purchase_detail_product.product_type",
                    "oa_dev.oa_purchase_detail_product.product_model",
                    "oa_dev.oa_purchase_detail_product.product_unit",
                    "oa_dev.oa_purchase_detail_product.product_num",
                    "oa_dev.oa_purchase_detail_product.product_price",
                    "oa_dev.oa_purchase_detail_product.product_total",
            };

            {
                SELECT(FIELDS);
                FROM("oa_dev.oa_purchase_apply");
                LEFT_OUTER_JOIN("oa_dev.oa_purchase_detail_product ON oa_dev.oa_purchase_detail_product.apply_product_id = oa_dev.oa_purchase_apply.apply_product_id AND (NOT oa_dev.oa_purchase_detail_product.del_flag)");
                LEFT_OUTER_JOIN("oa_dev.sys_user ON oa_dev.sys_user.user_id = oa_dev.oa_purchase_apply.apply_user_id");
                LEFT_OUTER_JOIN("oa_dev.sys_dept ON oa_dev.sys_dept.dept_id = oa_dev.oa_purchase_apply.apply_dept");

                //构建条件子句
                WHERE("oa_dev.oa_purchase_apply.apply_product_id = #{applyProductId}");
            }
        };
        String sqlStr = sql.toString();
        return sqlStr;
    }

    public String selectOaPurchaseApplyList(@Param("queryDto") OaPurchaseApplyDto queryDto) {
        SQL sql = new SQL() {

            private final String[] FIELDS = new String[]{
                    "oa_dev.oa_purchase_apply.apply_product_id",
                    "oa_dev.oa_purchase_apply.apply_user_id",
                    "oa_dev.sys_user.nick_name AS apply_user_name",
                    "oa_dev.oa_purchase_apply.apply_dept",
                    "oa_dev.oa_purchase_apply.apply_status",
                    "oa_dev.sys_dept.dept_name AS apply_dept_name",
                    "oa_dev.oa_purchase_apply.apply_time",
                    "oa_dev.oa_purchase_apply.total_amount",
                    "oa_dev.oa_purchase_apply.reason_for_purchase",
                    "oa_dev.oa_purchase_apply.status",
                    "oa_dev.oa_purchase_apply.remark",
                    "oa_dev.oa_purchase_apply.instance_id",
                    //新加字段
                    "oa_dev.oa_purchase_apply.apply_status",
            };

            {
                SELECT(FIELDS);
                FROM("oa_dev.oa_purchase_apply");
                LEFT_OUTER_JOIN("oa_dev.sys_user ON oa_dev.sys_user.user_id = oa_dev.oa_purchase_apply.apply_user_id");
                LEFT_OUTER_JOIN("oa_dev.sys_dept ON oa_dev.sys_dept.dept_id = oa_dev.oa_purchase_apply.apply_dept");

                //构建条件子句
                WHERE("NOT oa_dev.oa_purchase_apply.del_flag");
                if (queryDto.getApplyProductId() != null)
                    WHERE("oa_dev.oa_purchase_apply.apply_product_id = #{queryDto.applyProductId}");
                if (queryDto.getApplyUserId() != null)
                    WHERE("oa_dev.oa_purchase_apply.apply_user_id = #{queryDto.applyUserId}");
                if (queryDto.getApplyDept() != null)
                    WHERE("oa_dev.oa_purchase_apply.apply_dept = #{queryDto.applyDept}");
                if (queryDto.getApplyStatus() != null)
                    WHERE("oa_dev.oa_purchase_apply.apply_status = #{queryDto.applyStatus}");
                if (queryDto.getTotalAmount() != null)
                    WHERE("oa_dev.oa_purchase_apply.total_amount = #{queryDto.totalAmount}");
                if (StringUtils.hasText(queryDto.getReasonForPurchase()))
                    WHERE("oa_dev.oa_purchase_apply.reason_for_purchase = #{queryDto.reasonForPurchase}");
                if (StringUtils.hasText(queryDto.getStatus()))
                    WHERE("oa_dev.oa_purchase_apply.status = #{queryDto.status}");
                if (queryDto.getBeginTime() != null)
                    WHERE("oa_dev.oa_purchase_apply.apply_time >= #{queryDto.beginTime}");
                if (queryDto.getEndTime() != null) WHERE("oa_dev.oa_purchase_apply.apply_time <= #{queryDto.endTime}");

                //构建排序子句
                if (ArrayUtils.isNotEmpty(queryDto.getOrderByColumn())) ORDER_BY(queryDto.getOrderByColumn());

                //构建分页子句
                if (queryDto.getPageNum() != null && queryDto.getPageSize() != null) {
                    LIMIT(queryDto.getPageSize());
                    OFFSET((queryDto.getPageNum() - 1) * queryDto.getPageSize());
                }
            }
        };
        String sqlStr = sql.toString();
        return sqlStr;
    }

    public String selectOaPurchaseApplyTotal(@Param("queryDto") OaPurchaseApplyDto queryDto) {
        SQL sql = new SQL() {
            {
                SELECT("COUNT(0)");
                FROM("oa_dev.oa_purchase_apply");
                LEFT_OUTER_JOIN("oa_dev.sys_user ON oa_dev.sys_user.user_id = oa_dev.oa_purchase_apply.apply_user_id");
                LEFT_OUTER_JOIN("oa_dev.sys_dept ON oa_dev.sys_dept.dept_id = oa_dev.oa_purchase_apply.apply_dept");

                //构建条件子句
                WHERE("NOT oa_dev.oa_purchase_apply.del_flag");
                if (queryDto.getApplyUserId() != null)
                    WHERE("oa_dev.oa_purchase_apply.apply_user_id = #{queryDto.applyUserId}");
                if (queryDto.getApplyDept() != null)
                    WHERE("oa_dev.oa_purchase_apply.apply_dept = #{queryDto.applyDept}");
                if (queryDto.getTotalAmount() != null)
                    WHERE("oa_dev.oa_purchase_apply.total_amount = #{queryDto.totalAmount}");
                if (StringUtils.hasText(queryDto.getReasonForPurchase()))
                    WHERE("oa_dev.oa_purchase_apply.reason_for_purchase = #{queryDto.reasonForPurchase}");
                if (StringUtils.hasText(queryDto.getStatus()))
                    WHERE("oa_dev.oa_purchase_apply.status = #{queryDto.status}");
                if (queryDto.getBeginTime() != null)
                    WHERE("oa_dev.oa_purchase_apply.apply_time >= #{queryDto.beginTime}");
                if (queryDto.getEndTime() != null) WHERE("oa_dev.oa_purchase_apply.apply_time <= #{queryDto.endTime}");
            }
        };
        String sqlStr = sql.toString();
        return sqlStr;
    }

    public String insertOaPurchaseApply(OaPurchaseApply newOaPurchaseApply) {

        SQL sql = new SQL() {
            {
                INSERT_INTO("oa_purchase_apply");
                VALUES("apply_product_id", "#{applyProductId}");
                VALUES("create_by", "#{createBy}");
                VALUES("create_time", "#{createTime}");
                VALUES("update_by", "#{updateBy}");
                VALUES("update_time", "#{updateTime}");
                if (newOaPurchaseApply.getApplyUserId() != null) VALUES("apply_user_id", "#{applyUserId}");
                if (newOaPurchaseApply.getApplyDept() != null) VALUES("apply_dept", "#{applyDept}");
                if (newOaPurchaseApply.getApplyTime() != null) VALUES("apply_time", "#{applyTime}");
                if (newOaPurchaseApply.getTotalAmount() != null) VALUES("total_amount", "#{totalAmount}");
                VALUES("reason_for_purchase", "#{reasonForPurchase}");
                if (StringUtils.hasText(newOaPurchaseApply.getStatus())) VALUES("status", "#{status}");
                if (StringUtils.hasText(newOaPurchaseApply.getRemark())) VALUES("remark", "#{remark}");
            }
        };
        return sql.toString();
    }

    public String updateOaPurchaseApply(OaPurchaseApply modifiedOaPurchaseApply) {
        SQL sql = new SQL() {{
            UPDATE("oa_purchase_apply");
            SET("update_by = #{updateBy}");
            SET("update_time = #{updateTime}");
            SET("apply_user_id = #{applyUserId}");
            SET("apply_dept = #{applyDept}");
            SET("apply_time = #{applyTime}");
            SET("total_amount = #{totalAmount}");
            SET("reason_for_purchase = #{reasonForPurchase}");
            SET("remark = #{remark}");
            WHERE("apply_product_id = #{applyProductId}");
        }};
        return sql.toString();
    }

    public String removeOaPurchaseApplyByIds(final String[] applyProductIds, final String updateBy, final Date updateTime) {
        SQL sql = new SQL() {{
            UPDATE("oa_purchase_apply");
            SET("del_flag = '2'");
            if (StringUtils.hasText(updateBy)) SET("update_by = #{updateBy}");
            if (updateTime != null) SET("update_time = #{updateTime}");
            WHERE(String.format("apply_product_id IN (%s)", SqlUtil.formatSqlString(applyProductIds)));
        }};
        return sql.toString();
    }
}
```