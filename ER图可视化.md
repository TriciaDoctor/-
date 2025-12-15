# 明日方舟干员数据库 ER图

## 实体关系图

```mermaid
erDiagram
    Faction ||--o{ Operator : "所属1:N"
    Profession ||--o{ Operator : "担任N:1"
    Operator ||--o{ Operator_Stats : "拥有属性"
    Operator ||--o{ Skill : "掌握技能1:N"
    Skill ||--o{ Skill_Level : "技能提升1:N"
    Operator ||--o{ Talent : "拥有天赋N"
    Operator ||--o{ Elite_Material : "需要材料N:N"
    Material ||--o{ Elite_Material : "用于精英化N:1"
    Operator ||--o{ Potential : "提升潜能1:N"

    Faction {
        varchar faction_name PK "阵营名称"
        varchar race "种族"
    }

    Profession {
        varchar profession_name PK "职业名称"
        varchar branch_type "分支类型"
    }

    Operator {
        int operator_id PK "干员ID"
        varchar name "名字"
        varchar gender "性别"
        tinyint rarity "稀有度"
        varchar faction_name FK "阵营名称"
        varchar profession_name FK "职业名称"
    }

    Operator_Stats {
        int stat_id PK "属性ID"
        int operator_id FK "干员ID"
        tinyint elite_phase "精英化阶段"
        tinyint level "等级"
        int max_hp "生命值"
        int atk "攻击力"
        int def "防御力"
        int res "法术抗性"
        int deploy_cost "部署费用6星"
        tinyint block_count "阻挡数"
        decimal attack_speed "攻击速度"
    }

    Skill {
        int skill_id PK "技能ID"
        int operator_id FK "干员ID"
        varchar skill_name "技能名称"
        tinyint skill_index "技能序号1/2/3"
        varchar trigger_type "触发类型/自动手动"
        varchar recovery_type "回复类型/自动攻击受击"
    }

    Skill_Level {
        int skill_level_id PK "技能等级ID"
        int skill_id FK "技能ID"
        tinyint level "技能等级1-7"
        int sp_cost "SP消耗"
        int initial_sp "初始SP"
        int duration "持续时间"
    }

    Talent {
        int talent_id PK "天赋ID"
        int operator_id FK "干员ID"
        varchar talent_name "天赋名称"
        tinyint talent_index "天赋序号1/2"
        text talent_description "天赋描述"
    }

    Elite_Material {
        int elite_material_id PK "精英化材料ID"
        int operator_id FK "干员ID"
        int material_id FK "材料ID"
        int quantity "材料数量"
        int tlmd_cost "龙门币消耗"
        tinyint level_requirement "等级要求"
    }

    Material {
        int material_id PK "材料ID"
        varchar material_name "材料名称"
        tinyint rarity "稀有度"
        text obtain_method "获取途径"
    }

    Potential {
        int potential_id PK "潜能ID"
        int operator_id FK "干员ID"
        tinyint potential_level "潜能等级"
        text potential_effect "潜能效果描述"
    }
```

## 实体说明

### 基础实体
- **Faction（阵营）**：游戏中的各个势力组织
- **Profession（职业）**：干员的职业分类
- **Material（材料）**：游戏中的升级材料

### 核心实体
- **Operator（干员）**：游戏角色主体信息

### 从属实体
- **Operator_Stats（干员属性）**：干员在不同阶段的数值属性
- **Skill（技能）**：干员拥有的技能
- **Skill_Level（技能等级）**：技能在不同等级的效果
- **Talent（天赋）**：干员的被动能力
- **Potential（潜能）**：干员的潜能提升效果
- **Elite_Material（精英化材料）**：干员精英化所需材料清单

## 关系说明

1. **所属（1:N）**：一个阵营包含多个干员
2. **担任（N:1）**：多个干员担任同一职业
3. **拥有属性**：一个干员有多条属性记录
4. **掌握技能（1:N）**：一个干员掌握多个技能（最多3个）
5. **技能提升（1:N）**：一个技能有多个等级（1-7级）
6. **拥有天赋（N）**：一个干员拥有多个天赋（最多2个）
7. **需要材料（N:N）**：干员与材料的多对多关系
8. **用于精英化（N:1）**：材料用于多个干员的精英化
9. **提升潜能（1:N）**：一个干员有多个潜能等级（1-6级）
