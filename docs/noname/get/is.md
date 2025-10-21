# Class "is"

你可以通过以下方式调用这个类：

```javascript
get.is
```

## 方法
### xingDong(event)

判断事件是否属于“行动”类事件，包括直接行动和父事件标识为攻击或法术的情况。

### gongJi(event)

判断是否为一次攻击行为（含目标）。

### yingZhanGongJi(event)

判断是否为“应战攻击”。

### zhuDongGongJi(event)

判断是否为“主动攻击”。

### gongJiXingDong(event)

判断是否为“攻击行动”，与 zhuDongGongJi 语义上相同，用于逻辑区分。

### faShuXingDong(event)

判断事件是否为“法术行动”，支持通过技能或卡牌触发的判断。

```javascript
let event = {
    name: 'useCard',
    card: { name: 'fireball' }
};
if (get.type(event.card) == 'faShu' && get.is.xingDong(event)) {
    console.log("这是一次法术行动");
}
```

### gongJiShangHai(event)

判断当前事件是否为攻击造成的伤害（非法术）。

### faShuShangHai(event)

判断当前事件是否为法术造成的伤害。