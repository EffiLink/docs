# Source: https://developers.effilink.co/api-reference/v5/property.html

**联系人的系统预定义属性**

| 名称 | 类型 | 标识 | 描述 | 示例值 |
| --- | --- | --- | --- | --- |
| **姓名** | string | **name** | 联系人名称 | 张三 |
| **邮箱地址** | string | **email** | 联系人的邮箱地址 | zhangsan@easeye.com.cn |
| **手机号码** | string | **phoneNumber** | 联系人的联系电话 | 13800000000 |
| **最后触达时间** | date | **properties.touch\_time** | 触达时间 | 2023-03-11 13:00:00 |
| **来源** | string | **properties.source** | 联系人来源 | 文件导入 |
| **公司名称** | string | **properties.company** | | 公司名称Example |
| **公司地址** | string | **properties.company\_address** | | 上海市浦东新区xx路xx号 |
| **生命周期阶段** | string | **properties.lifecycle\_stage** | | |
| **所在地域** | string | **properties.city** | | |
| **行业/部门** | string | **properties.industry** | | IT |
| **阶段变更时间** | date | **properties.lead\_response\_time** | | 2023-03-11 13:00:00 |
| **生日** | date | **properties.birthday** | | 2000-03-11 13:00:00 |
| **邮件过滤状态** | string | **properties.email\_bounced\_flag** | | 取值范围：0，1，2，3，100，1000。0（正常），1（硬退过滤），2（退订过滤），3（投诉过滤），100(管理员过滤)，1000（系统强制过滤） |
| **邮件过滤时间** | date | **properties.email\_bounced\_time** | | 2023-03-11 13:00:00 |
| **邮件打开次数** | int | **properties.email\_open\_count** | | 1 |
| **邮件最后打开时间** | date | **properties.email\_open\_last\_time** | | 2023-03-11 13:00:00 |
| **邮件点击次数** | int | **properties.email\_click\_count** | | 1 |
| **邮件最后点击时间** | date | **properties.email\_click\_last\_time** | | 2023-03-11 13:00:00 |