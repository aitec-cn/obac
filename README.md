# OBAC
Orgnazition Based Access Control Model,Aims at 2B  software application .


## 权限设计OBAC模型）
1. 模型
    - 组织（orgnazition）多层次组织。每个用户属于一个组织，每一个资源属于一个组织，一个用户可以访问同一个组织内的资源，并根据角色确定访问范围等级
    - 资源(resource) resource为数据资源， 如：订单信息、客户信息等，通过组织ID实现在不同组织层级的数据隔离。
    - 
    - 动作(action) action为对resource的操作权限,通过web路径来区分resource+action，如：创建、查看、修改、删除等。
    - 角色(role) role为组织下的角色，不同的user属于不同的role，role又是不同层级下的role，一个role可以覆盖多个resource，role可以对应多个action。
    - 作用域(scope) tenant、group、company、individual(user)等均为不同层级的组织作用域，组织的关系为树形结构。

2. 实现
    - 创建一个action、resource、role、scope 四元组表，用于存储和判别某动作所需的组织角色和作用域（组织层级）。（对于简单的应用，把role加入到url path里，实现通过路径提取该action对应的四元组）
    - 默认所有action，在数据库操作层面都加入对应层级的org_id，以实现数据隔离。 
    - 同一组织下，管理员可以忽略低层级的orgID,以实现对其他普通成员的数据操作。
    - 每一个请求的token里都需要携带多层级的org id（如tenantId GroupID companyId UsrId 等），role，userid 等，以确认是否满足权限判别。

