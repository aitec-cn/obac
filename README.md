# ORRA
Orgnization-Role-Resource-Action Based Access Control Model,Aims at 2B  software application .


# 权限设计（ORRA模型）
1. 模型
    - 组织(org) tenant、group、company、individual(user)等均为不同层级的组织，组织的关系为树形结构。
    - 资源(rsc) resource为数据资源， 如：订单信息、客户信息等，通过组织ID实现在不同组织层级的数据隔离。
    - 角色(role) role为组织下的角色，不同的user属于不同的role，role又是不同层级下的role，一个role可以覆盖多个resource，role可以对应多个action。
    - 动作(action) action为对resource的操作权限,通过web路径来区分resource+action，如：创建、查看、修改、删除等。
2. 实现
    - 创建一个org、role、action 三元组表，用于存储和判别某动作所需的组织角色。（对于简单的应用，把role加入到action（path）里，实现通过路径提取该action对应的三元组）
    - 每一个请求的token里都需要携带多层级的org id（如tenantId GroupID companyId UsrId 等），role，userid 等，以确认是否满足权限判别。
    - 默认所有action，在数据库操作层面都加入对应层级的org_id，以实现数据隔离。
    - 同一组织下，管理员可以忽略低层级的orgID,以实现对其他普通成员的数据操作。
 

