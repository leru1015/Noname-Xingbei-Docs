# Class "Player"

本文档介绍Player类的经常使用的属性和方法，全部属性和方法请参考源码
文件路径：noname/library/element/player.js

## 属性

### zhiLiao

玩家治疗数量，数值
```javascript
var zhiLiaoNum=player.zhiLiao; //2
```

### storage

玩家存储区，字典，常用于存储各种自定义属性
```javascript
player.storage['test']='myValue';
if(player.storage['test']=='myValue'){
    //do something
}
```

### group

玩家势力，字符串
```javascript
var playerGroup=player.group; //'yongGroup'
```

### side

玩家队伍位置，布尔值，true为红方，false为蓝方
```javascript
var playerSide=player.side; //true
```

### name

玩家角色id，字符串
```javascript
var characterId=player.name; //'fengZhiJianSheng'
```

### next

玩家下家，Player对象
```javascript
var nextPlayer=player.next; //Player对象
```

### previous

玩家上家，Player对象
```javascript
var previousPlayer=player.previous; //Player对象
```

## 非事件函数

### init(character)

初始化玩家角色
```javascript
player.init('fengZhiJianSheng');
```

### getCards(arg1, arg2)

获取角色特定区域的牌
获取角色特定区域的牌数
支持参数分别为
- 位置字符串('h'，'x'(盖牌等))
- 函数(卡牌筛选，card=>get.xiBie=='di'&&get.type(card)=='gongJi')，若未设置位置字符串，默认为'h'
返回值为列表
```javascript
player.getCards('h'); //[card1,card2,card3]
```

### countCards(arg1, arg2)

获取角色特定区域的牌数
支持参数分别为
- 位置字符串('h'，'x'(盖牌等))
- 函数(卡牌筛选，card=>card.name=='anMie')，若未设置位置字符串，默认为'h'
返回值为属数值
```javascript
player.countCards('h',card=>get.mingGe(card)=='xue'); //3
```

### hasCard(name, position)

判断角色是否拥有某张牌
支持参数分别为
- 筛选条件(字符串、函数)
- 位置字符串('h'，'x'(盖牌等))，若未设置位置字符串，默认为'h'
返回值为布尔
```javascript
player.hasCard('anMie','h'); //true
```

### addGongJiOrFaShu(num)

角色获得额外num个攻击或法术行动，num默认为1
返回值为增加后的攻击或者法术行动数量
```javascript
player.addGongJiOrFaShu(2); //2
```

### addGongJi(num)

角色获得额外num个攻击行动，num默认为1
返回值为增加后的攻击行动数量
```javascript
player.addGongJi(); //1
```

### addFaShu(num)

角色获得额外num个法术行动，num默认为1
返回值为增加后的法术行动数量
```javascript
player.addFaShu(); //1
```

### hasJiChuXiaoGuo(jiChuXiaoGuo)

判断角色是否拥有某种基础效果；若无jiChuXiaoGuo参数，则判断是否拥有任意基础效果
返回值为布尔值
```javascript
player.hasJiChuXiaoGuo('zhongDu'); //false
```

### jiChuXiaoGuoList()

获取角色当前的所有基础效果
返回值为数组
```javascript
player.jiChuXiaoGuoList(); //['_shengDun','xunJieCiFu_xiaoGuo']
```

### canTeShu()

判断角色是否能执行特殊行动，主要用于ai判断
返回值为布尔值
```javascript
player.canTeShu(); //true
```

### canFaShu()

判断角色是否能执行法术行动，包含法术技能，主要用于ai判断
返回值为布尔值
```javascript
player.canFaShu(); //false
```

### canGongJi()

判断角色是否能执行攻击行动，主要用于ai判断
返回值为布尔值
```javascript
player.canGongJi(); //true
```

### canXingDong(type)

判断角色是否能执行某个行动，主要用于ai判断
若无type参数，则判断是否能执行任意行动，type可选值为"gongJi"、"faShu"、"teShu"
返回值为布尔值
```javascript
player.canXingDong(); //true
player.canXingDong('faShu'); //false
```

### isHengZhi()

是否横置（在星杯里一般是进形态），可用于判断某个角色是否在形态内
返回值为布尔值
```javascript
player.isHengZhi(); //false
```

### getZhiLiaoLimit()

获得角色治疗上限数
返回值为数值
```javascript
player.getZhiLiaoLimit(); //3
```

### getNengLiangLimit()

获得角色能量上限数
返回值为数值
```javascript
player.getNengLiangLimit(); //3
```

### getHandcardLimit()

获得角色手牌上限数
返回值为数值
```javascript
player.getHandcardLimit(); //5
```

### canBiShaShuiJing()

判断角色是否能发动需要水晶的技能（通常用于filter）
返回值为布尔
```javascript
player.canBiShaShuiJing(); //true
```

### canBiShaBaoShi()

判断角色是否能发动需要宝石的技能（通常用于filter）
返回值为布尔
```javascript
player.canBiShaBaoShi(); //false
```

### countTongXiPai(type)

统计同系牌的数量，type可选值为'gongJi'和'faShu'，设置type后只统计该类型的同系牌，不设置则统计所有同系牌
返回值为数值
```javascript
player.countTongXiPai('faShu'); //2
```

### countYiXiPai(type)

统计异系牌的数量，type可选值为'gongJi'和'faShu'，设置type后只统计该类型的异系牌，不设置则统计所有异系牌
返回值为数值
```javascript
player.countYiXiPai('gongJi'); //3
```

### countTongMingPai()

统计同命格牌的数量
返回值为数值
```javascript
player.countTongMingPai(); //4
```

### countYiMingPai()

统计不同命格牌的数量
返回值为数值
```javascript
player.countYiMingPai(); //1
```

### countEmptyCards()

统计角色还差多少张牌才能达到手牌上限
返回值为数值
```javascript
player.countEmptyCards(); //2
```

### countEmptyNengLiang()

统计角色还差多少个星石才能达到能量上限
返回值为数值
```javascript
player.countEmptyNengLiang(); //1
```

### countNengLiang(xingShi)

获取角色当前的某个类型的星石数
返回值为数值
```javascript
player.countNengLiang('shuiJing'); //2
```

### hasNengLiang(xingShi)

判断角色是否有某个类型的星石，若无xingShi参数，则判断是否有任意类型的星石
返回值为布尔值
```javascript
player.hasNengLiang('baoShi'); //false
```

### countNengLiangAll()

获取角色的所有星石数
返回值为数值
```javascript
player.countNengLiangAll(); //3
```

### countZhiShiWu(zhiShiWu)

获取指示物的数量
支持参数：
- 字符串：指示物id
返回值为数值
```javascript
var num=player.countZhiShiWu('xxx'); //3
```

### isZhiShiWuMax(zhiShiWu)

判断指示物是否到达上限
支持参数：
- 字符串：指示物id
返回值为布尔值
```javascript
var isMax=player.isZhiShiWuMax('xxx'); //false
```

### hasZhiShiWu(zhiShiWu)

判断角色是否拥有某个指示物
支持参数：
- 字符串：指示物id
返回值为布尔值
```javascript
var has=player.hasZhiShiWu('xxx'); //false
```

### usedSkill(skill)

判断角色本回合是否使用过某个技能
支持参数：
- 字符串：技能id
返回值为布尔值
```javascript
var used=player.usedSkill('xxx'); //true
```

### countSkill(skill)

统计角色本回合使用某个技能的次数
支持参数：
- 字符串：技能id
返回值为数值
```javascript
var count=player.countSkill('xxx'); //2
```

### getGaiPai(gaintag)

获取角色的某种盖牌
支持参数：
- 字符串：盖牌id
返回值为列表
```javascript
var cards=player.getGaiPai('xxx'); 
//[card1,card2,card3]
```

### countGaiPai(gaintag)

统计角色的某种盖牌数量
支持参数：
- 字符串：盖牌id
返回值为数值
```javascript
var count=player.countGaiPai('xxx'); //3
```

### hasGaiPai(gaintag)

判断角色是否拥有某种盖牌
支持参数：
- 字符串：盖牌id
返回值为布尔值
```javascript
var has=player.hasGaiPai('xxx'); //true
```

### getJiChuXiaoGuo(jiChuXiaoGuo)

获取角色某种基础效果的卡牌
支持参数：
- jiChuXiaoGuo：字符串，基础效果id
返回值为列表
```javascript
var result=await player.getJiChuXiaoGuo('_shengDun');
//[card1]
```

### countJiChuXiaoGuo(jiChuXiaoGuo)

统计角色某种基础效果的数量
支持参数：
- jiChuXiaoGuo：字符串，基础效果id
返回值为数值
```javascript
var result=await player.countJiChuXiaoGuo('_shengDun'); //1
```

### countHong()

统计角色的红色指示物数量
返回值为数值
```javascript
var count=player.countHong(); //2
```

### countLan()

统计角色的蓝色指示物数量
返回值为数值
```javascript
var count=player.countLan(); //1
```

### hasSkill(skill,arg2, arg3, arg4)

判断角色是否拥有某个技能，剩余参数暂未使用
支持参数：
- skill：字符串，技能id
- 布尔值1
返回值为布尔值
```javascript
var has=player.hasSkill('xxx'); //true
```
### addSkill(skill, checkConflict, nobroadcast, addToSkills)

玩家添加技能
支持参数：
- skill：字符串，技能id
- checkConflict：布尔值，是否检查技能冲突，目前星杯里没实际用途
- nobroadcast：布尔值，是否不广播技能添加，用于隐藏技能
- addToSkills：布尔值，是否添加到玩家技能列表
```javascript
player.addSkill('xxx');
```

### removeSkill(skill)

玩家移除技能
支持参数：
- 字符串：技能id
```javascript
player.removeSkill('xxx');
```

### addTempSkill(skill, expire, checkConflict)

玩家添加临时技能，默认在回合开始/结束时移除
支持参数：
- skill：字符串，技能id
- expire：字符串/字典，移除时机('phaseBegin'，'gongJiEnd',{player:'faShuEnd'}等，和技能时机类似)
- checkConflict：布尔值，是否检查技能冲突，目前星杯里没实际用途
```javascript
player.addTempSkill('xxx',{player:'teShuEnd'});
```

### addSkillLog(skill,popup = true)

玩家添加技能并有日志
支持参数：
- skill：字符串，技能id
- popup：布尔值，玩家是否弹出技能名，和发动技能时的弹出一致，默认为true
```javascript
player.addSkillLog('xxx');
```

### removeSkillLog(skill, popup = true)

玩家移除技能并有日志
支持参数：
- skill：字符串，技能id
- popup：布尔值，玩家是否弹出技能名，和发动技能时的弹出一致，默认为true
```javascript
player.removeSkillLog('xxx');
```

### addAdditionalSkill(skill, skillsToAdd, keep)

玩家添加附加技能
支持参数：
- skill：字符串，附加技能存储列表
- skillsToAdd：字符串/列表，要添加的技能id
- keep：布尔值，是否保留原有的附加技能，默认为false
```javascript
player.addAdditionalSkill('myExtraSkills','xxx');
```

### removeAdditionalSkill(skill, target)

玩家移除附加技能
支持参数：
- skill：字符串，附加技能存储列表
- target：字符串/列表，要移除的技能id
```javascript
player.removeAdditionalSkill('myExtraSkills','xxx');
```

### tempBanSkill(skill, expire, log)

玩家临时封禁技能，默认在回合开始/结束时解封
支持参数：
- skill: 字符串，技能id
- expire: 字符串/字典，解封时机('phaseBegin'，'gongJiEnd',{player:'faShuEnd'}等，和技能时机类似，如果为'forever'则永久封印)
- log: 布尔值，是否有日志，默认有日志
```javascript
player.tempBanSkill('xxx','forever')
```

### isTempBanned(skill)

判断某个技能是否被封印
支持参数：
- skill：字符串，技能id
返回值为布尔值
```javascript
player.isTempBanned('xxx');//true
```

### isOnline()

判断角色是否在线并且未托管
返回值为布尔值
```javascript
var online=player.isOnline(); //true
```

### isOnline2()

判断角色是否在线，包含托管状态
返回值为布尔值
```javascript
var online=player.isOnline2(); //true
```

### isOffline()

判断角色是否离线
返回值为布尔值
```javascript
var offline=player.isOffline(); //false
```

### canUseXingBei(card, target)

判断角色是否对target使用card
支持参数
- card：卡牌
- target：玩家
返回值布尔
```javascript
player.canUseXingBei(card,target)//true
```

### hasUseTargetXingBei(card)

判断场上是否存在能成为card的目标
支持参数
- card：卡牌
返回值布尔
```javascript
player.hasUseTargetXingBei(card)//true
```

### 以下函数请参加函数源码

因使用较少，本文档暂不详细说明，且都可存在明显等价替代方法
文件路径：noname/library/element/player.js

### getRoundHistory()

### getHistory()

### checkHistory()

### hasHistory()

### getLastHistory()

### checkAllHistory()

### getAllHistory()

### hasAllHistory()

### getLastUsed()

### getStat()

### getLastStat()

### setStorage(name, value, mark)

设置角色的存储数据，等价于player.storage[name]=value
支持参数：
- name：字符串，存储名称
- value：任意，存储值
- mark：布尔值，是否显示标记，默认为不显示
```javascript
player.setStorage('myKey', 'myValue');
```

### getStorage(name, defaultValue = [])

获取玩家的存储数据，等价于player.storage[name]
支持参数：
- name：字符串，存储名称
- defaultValue：任意，默认为空列表，当存储值未定义时返回该值
```javascript
var value=player.getStorage('myKey'); //'myValue'
```

### hasStorageAny()

### hasStorageAll()

### initStorage()

### updateStorage()

### updateStorageAsync()

### removeStorage()

## 事件函数
多数返回值为事件，极少无返回值
本页面中带NoTrigger标记的的函数无Before/Begin/End/After时机触发器
部分函数有高级使用方法，本文档暂不会涉及，使用可参考技能源码或者查看函数定义
针对选择函数的ai行为，本文档暂不会过多讲解，使用可参考技能源码
参数列表中某些类别的参数分1，2，这些参数有前后顺序要求，第一个被传入的这类参数就被用为参数1，依次类推
事件函数可用set()函数设置特定属性，部分函数通过传参只能传入部分参数，可以用set()设置其他参数
选择函数在异步函数中使用时，需使用await关键字等待选择结果返回，并且使用forResult()函数获取结果
事件函数的具体执行过程参见文件：noname/library/element/content.js
```javascript
let result = await player.chooseToDiscard(2,'h').forResult();
/*
result = {
    bool: true, //是否选择了弃牌
    cards: […], //弃掉的牌
}
可在forResult()中设置参数来获取特定结果，如targets、cards等
forResult('targets') //获取选择的目标
forResult('cards','targets') //获取选择的卡牌和目标的数组
这些函数可直接返回对应的值
forResultBool()
forResultTargets()
forResultCards()
forResultControl()
forResultLinks()
*/
```

### reinitCharacter(from, to, log = true)

玩家重新初始化角色
支持参数
- from：字符串，原角色id
- to：字符串，新角色id
- log：布尔值，是否有日志，默认为true
```javascript
player.reinitCharacter('zhuLvZhe','hongYiZhuJiao');
```

### chooseToDiscard()

玩家选择弃牌
支持参数
- 数值/范围列表(弃牌数/范围，2,[1,2],弃2张、弃1~2张)-
- 位置字符串('h'，星杯里目前就h有用)、布尔值(是否必须弃牌)-
- 函数1(卡牌过滤器、function(card)返回值为true则可以选择)
- 函数2(ai)、字典(可代替函数1来删选牌、{xiBie:'shui'})
- 字符串('showCards','showHiddenCards'，提示文本，前两个为展示弃牌，第一个展示触发封印师封印，第二个不触发封印；提示文本任意，会在选择弃牌弹窗中显示)
```javascript
'step 0' 
player.chooseToDiscard([1,2],'h',true,card=>get.mingGe(card)=='xue','showCards','测试技能：弃置1到2张血命格手牌').set('ai',(card)=>{
    return 10-get.value(card);//优先弃掉价值低的牌，返回值为本卡牌的选择优先级
});
//玩家必须弃掉1到2张血命格手牌，并且弃牌展示，ai优先弃掉价值低的牌，弹窗为"测试技能：弃置1到2张血命格手牌"
'step 1'
console.log(result); //玩家弃掉的牌
/*
result = {
    bool: true, //是否选择了弃牌
    cards: […], //弃掉的牌
}
*/
```

### chooseCard()

玩家选择弃牌
支持参数
- 数值/范围列表(选择牌数/范围，2,[1,2],弃2张、弃1~2张)
- 位置字符串('h'，星杯里目前就h有用)、布尔值(是否必须选择)
- 函数1(卡牌过滤器、function(card)返回值为true则可以选择)
- 函数2(ai)、字典(可代替函数1来删选牌、{xiBie:'shui'})、字符串(提示文本，提示文本任意，会在选择弃牌弹窗中显示)
```javascript
var result=await player.chooseCard(2,'h',card=>get.xiBie(card)=='huo','测试技能：选择2张火系手牌').set('ai',(card)=>{
    if(_status.event.player.countCards('h',card=>get.xiBie(card))>2){
        return 10-get.value(card);
    }else return 0;
    //如果手中火系牌数大于2，则选择，否则不选择
}).forResult();
//玩家选择1到2张火系手牌，弹窗为"测试技能：选择2张火系手牌"

console.log(result); //玩家弃掉的牌
/*
result = {
    bool: true, //是否选择了牌
    cards: […], //选择的牌
}
*/
```

### chooseTarget()

玩家选择目标
支持参数
- 数值/范围列表(选择目标数/范围，2,[1,2],选2个、选1~2个)-
- 布尔值(是否必须选择)
- 函数1(目标过滤器、function(target)返回值为true则可以选择)
- 函数2(ai)、字符串(提示文本，提示文本任意，会在选择目标弹窗中显示)
```javascript
var result=await player.chooseTarget(1,true,lib.filter.opponent,'测试技能：选择1个目标对手弃1张牌').set('ai',(target)=>{
    return target.countCards('h'); //优先选择手牌数多的目标
}).forResult();

console.log(result); //玩家选择的目标
/*
result = {
    bool: true, //是否选择了目标
    targets: […], //选择的目标
}
*/
```

### chooseCardTarget(choose)

玩家同时选择卡牌和目标
choose为一个字典，多使用以下键名：
- filterCard：卡牌过滤器，function(card)，未设置则默认全部可选
- filterTarget：目标过滤器，function(target,player,card)，未设置则默认全部可选
- selectCard：选择卡牌数/范围，数值/范围列表，2,[1,2]，未设置默认为1
- selectTarget：选择目标数/范围，数值/范围列表，2,[1,2]，未设置默认为1
- ai1：卡牌ai，function(card)，未设置默认为使用价值
- ai2: 目标ai，function(target)，未设置默认优先友方
- 布尔值(是否必须选择)
```javascript
var result=await player.chooseCardTarget({
    filterCard:card=>get.xiBie(card)=='shui',
    filterTarget:target=>target!=player,
    selectCard:[1,2],
    selectTarget:1,
    ai1:card=>10-get.value(card),
    ai2:target=>10-target.countCards('h'),
}).forResult();
console.log(result); //玩家选择的卡牌和目标
/*
result = {
    bool: true, //是否选择了卡牌和目标
    cards: […], //选择的卡牌
    targets: […], //选择的目标
}
*/
```

### chooseControl()

玩家选择选项
支持参数
- 列表(选项列表，['选项1','选项2','选项3'])
- 字符串(增加到选项列表中)
- 函数(ai，function(event,player)，返回数值则使用列表对应索引的值，返回字符串则作为选择结果)
- 数值(默认为0，若无ai参数，则ai选择该索引的选项)
```javascript
var result=await player.chooseControl(['选项A','选项B'],1).set('prompt','测试技能：请选择一个选项').forResult();//ai优先选择选项B

console.log(result); //玩家选择的选项
/*
result = {
    control: '选项B' //选择的选项
}
*/

```

### chooseControlList()

玩家选择列表中的一个选项，根据了列表长度生成选项(选项1、选项2)
支持参数
- 列表(选项列表，['获得1水晶','战绩区增加1宝石'])
- 字符串(提示文本，提示文本任意，会在选择弹窗中显示)
- 函数(ai，function(event,player)，返回数值则使用列表对应索引的值，返回字符串则作为选择结果)
- 布尔值(是否必须选择，默认为false，会在选项里增加"cancel2"(取消)选项)
```javascript
var list = ['获得1水晶','战绩区增加1宝石'];
var result=await player.chooseControlList(list).set('ai',(event,player)=>{
    if(get.zhanJi(player.side).length>3) return '选项一'//根据玩家阵营的战绩区星石数量判断选项
    else return '选项二'
}).set('prompt','测试技能：请选择一个选项').forResult();

console.log(result); //玩家选择的选项
/*
result = {
    control: '选项二' //选择的选项
}
*/

```

### chooseButton()

玩家选择按钮
支持参数
- 布尔值1(是否必须选择)
- 布尔值2(是否是复杂选择，如果为true，则每次选择后会再次使用函数1筛选，默认为false)
- 数值/范围列表(选择按钮数/范围，2,[1,2],选2个、选1~2个)
- 函数1(按钮过滤器、function(button)返回值为true则可以选择)
- 函数2(ai，function(button)，返回值要为数值，为每个按钮选择优先级)
- 列表(按钮列表，[提示文本,[列表,创建样式字符串]]，['提示文本',[list,'tdnodes']])
    - 样式字符有以下，创建时，列表内变量类型要和样式对应
    - tdnodes：常用类型，可用于显示文本和数值
    - card：显示卡牌
    - blank：和card类似，但显示为牌背
    - vcard：显示虚拟牌
    - character：显示角色
    - characterx：显示角色（可切换为同名角色）
    - player：显示玩家
    - text：显示文本
```javascript
var list=get.zhanJi(player.side);//['baoShi','shuiJing','shuiJing']
var listx=[];
for(var i=0;i<list.length;i++){
    listx.push([list[i],get.translation(list[i])]);
};//[['baoShi','宝石'],['shuiJing','水晶'],['shuiJing','水晶']]
//列表中的翻译将用于显示，实际返回值为前面的字符串
var next=player.chooseButton([
    '选择移除的星石',
    [listx,'tdnodes'],
],true,[1,2]);
next.set('ai',(button)=>{
    if(button.link=='shuiJing') return 10; //优先选择水晶
    else return 1;
});
var result=await next.forResult();

console.log(result); //玩家选择的按钮
/*
result = {
    bool: true, //是否选择了按钮
    links: […], //选择的按钮
}
*/
```

### chooseCardButton()

玩家选择卡牌按钮
支持参数
- 卡牌列表
- 布尔值(是否必须选择)
- 字符串(提示文本)
- 数值/范围列表(选择按钮数/范围，2,[1,2],选2个、选1~2个)
```javascript
var cards=player.getGaiPai('xxx');
var result=await player.chooseCardButton(cards,2,'测试技能：是否移除2张【xxx】');

console.log(result);
/*
result = {
    bool: true, //是否选择了按钮
    links: […], //选择的卡牌
}
*/
```

### chooseButtonTarget(choose)

玩家同时选择按钮和目标
choose为一个字典，多使用以下键名：
- createDialog：同chooseButton里参数列表
- filterButton：按钮过滤器，function(button)，未设置则默认全部可选
- filterTarget：目标过滤器，function(target,player,card)，未设置则默认全部可选
- selectButton：选择按钮数/范围，数值/范围列表，2,[1,2]，未设置默认为1
- selectTarget：选择目标数/范围，数值/范围列表，2,[1,2]，未设置默认为1
- ai1：按钮ai，function(button)，未设置所有按钮优先级默认为1
- ai2：目标ai，function(target)，未设置默认优先友方
```javascript
var list=get.zhanJi(player.side);
var listx=[];
for(var i=0;i<list.length;i++){
    listx.push([list[i],get.translation(list[i])]);
}

let result=await player.chooseButtonTarget({
    createDialog:[
        '是否移除1个星石将一名其他角色手牌调整为4张[强制]',
        [listx,'tdnodes'],
    ],
    filterTarget:lib.filter.notMe,
    ai1:function(button){
        return -1;
    },
    ai2:function(target){
        if(target.countCards('h')==4) return -1;
        return Math.random();
    },
}).forResult();

console.log(result);
/*
result = {
    bool: true, //是否选择了按钮和目标
    links: […], //选择的按钮
    targets: […], //选择的目标
}
*/
```

### chooseButtonCard()

玩家同时选择按钮和卡牌，暂无技能使用
choose为一个字典，多使用以下键名：
- createDialog：同chooseButton里参数列表
- filterButton：按钮过滤器，function(button)，未设置则默认全部可选
- filterCard：卡牌过滤器，function(card)，未设置则默认全部可选
- selectButton：选择按钮数/范围，数值/范围列表，2,[1,2]，未设置默认为1
- selectCard：选择按钮数/范围，数值/范围列表，2,[1,2]，未设置默认为1
- ai1：目标选择ai
- ai2：选择卡牌ai
```javascript
let result=await player.chooseButtonCard({
    createDialog:[
        '移除1个星石和弃置1张手牌',
        [['baoShi','宝石'],['shuiJing','水晶'],'tdnodes'],
    ],
    ai1:function(button){
        return -1;
    },
    ai2:function(card){
        return -get.value(card);
    },
}).forResult();

console.log(result);
/*
result = {
    bool: true, //是否选择了按钮和卡牌
    links: […], //选择的按钮
    cards: […], //选择的卡牌
}
*/
```
### chooseDraw(num,bool)

玩家选择摸一定数量牌
支持参数：
- num：最多摸几张，默认为1
- bool：是否包含中间的数值
```javascript
var result=await player.chooseDraw(4,true).forResult;

console.log(result);
/*
result={
    control:num,摸了几张
}
*/
```

### chooseToGive()

玩家选择给予牌
支持参数：
- 玩家：接受牌的玩家
- 数值/范围列表：给予牌数/范围，2,[1,2],给2张、给1~2张
- 布尔值：是否必须给予
- 函数1：卡牌过滤器、function(card)返回值为true则可以选择
- 函数2：ai
- 字典：可代替函数1来删选牌，{xiBie:'shui'}

### discard()

玩家弃置牌，可set('sheQi',true)则无弃牌(dicard)触发器，也被常用于弃置盖牌和基础效果
支持参数：
- player：弃牌来源，默认无需设置
- cards/card：弃置的牌，单张或多张
- position：弃置去向(ui.ordering(处理区))，默认无需设置
- 字符串：('showCards','showHiddenCards',盖牌id)，前两个展示牌，前者触发封印，后者不触发，盖牌id用于弃置盖牌时显示日志用
```javascript
var cards=player.getGaiPia('xxx')
player.discard(cards,'xxx');
//日志：xx玩家弃置了x张【xxx】
```

### randomDiscard()

玩家随机弃置牌，暂无技能使用
支持参数：
- 数值：弃置数量
```javascript
player.randomDiscard(2);
```

### lose()

玩家失去牌，可set('sheQi',true)则无弃牌(dicard)触发器
支持参数：
- player：弃牌来源，默认无需设置
- cards/card：弃置的牌，单张或多张
- position：弃置去向(ui.ordering(处理区))，默认无需设置
```javascript
await player.lose(cards,ui.ordering);
//卡牌进临时区，用于后续技能处理
```

### draw()

玩家摸牌，部分参数未列出
支持参数：
- 数值：摸牌数量，默认为1
- 玩家：导致摸牌来源，根据需要设置
- 布尔值：牌面是否可见
```javascript
player.draw(3); //摸3张牌
```

### drawTo(num,arg)

玩家摸牌直到手牌数达到num
支持参数：
- num：手牌数
- arg：参数列表，用于设置draw函数
```javascript
player.drawTo(5); //摸牌直到手牌数达到5
```

### gain()

玩家获得牌，部分参数未列出
支持参数：
- cards/card：获得的牌，单张或多张
- 玩家：牌来源，根据需要设置
- 字符串：'log'，是否有日志，默认为false；动画方式('gain2','draw2','gain'等)，如果为'gain2'或'draw2'则log为true
```javascript
var cards=…;
await player.gain(cards,'log');
//日志：xx玩家获得了x张牌
```

### give(target,cards,visible)

玩家给予target牌
支持参数：
- target：接受牌的玩家
- cards/card：给予的牌，单张或多张
- visible：布尔值，牌是否明示，默认为false
```javascript
var cards=…;
await player.give(targetPlayer,cards);
```

### tiaoZhengShouPai(num)

玩家调整手牌至num张
支持参数：
- num：手牌数
```javascript
player.tiaoZhengShouPai(3); //调整手牌至3张
```

### damage(num,source)

玩家受到攻击伤害
支持参数：
- num：伤害数值，默认为1
- 玩家：伤害来源，根据需要设置
```javascript
await player.damage(2,sourcePlayer);
```

### faShuDamage(num,source)

玩家受到法术伤害
支持参数：
- num：伤害数值，默认为1
- 玩家：伤害来源，根据需要设置
```javascript
await player.faShuDamage(1,sourcePlayer);
```

### addGaiPai()

玩家增加盖牌
支持参数：
- cards/card：增加的盖牌，单张或多张
- 玩家：盖牌来源，根据需要设置
- 字符串：盖牌id
- 布尔值：是否为展示盖牌，默认为调取盖牌属性中show属性
```javascript
var cards=…;
await player.addGaiPai(cards,sourcePlayer,'xxx');
//日志：xx玩家获得了x张展示的【xxx】盖牌
```

### addJiChuXiaoGuo()

玩家增加基础效果，添加封印请使用addFengYin()
支持参数：
- cards/card：增加的盖牌，单张或多张
- 玩家：基础效果来源，根据需要设置
- 字符串：基础效果id
- 布尔值：是否有日志，默认为true
```javascript
var cards=…;
await player.addJiChuXiaoGuo(cards,'_shengDun');
```

### gainJiChuXiaoGuo(target)

NoTrigger，事件结束有触发器 gainJiChuXiaoGuo
玩家获得某个角色某个基础效果
事件result包含xiaoGuo和card属性，分别表示获得的基础效果和获取的卡牌
```javascript
var result=await player.gainJiChuXiaoGuo(event.target).forResult;

console.log(result);
/*
result = {
    xiaoGuo: '_zhongDu',
    card: ……
}
*/
```

### removeJiChuXiaoGuo(target)

NoTrigger，事件结束有触发器 removeJiChuXiaoGuo
玩家移除某个角色的某个基础效果
事件result包含xiaoGuo和card属性，分别表示获得的基础效果和移除的卡牌

```javascript
var result=await player.removeJiChuXiaoGuo(event.target).forResult;

console.log(result);
/*
result = {
    xiaoGuo: '_zhongDu',
    card: ……
}
*/
```

### insertPhase(skill, insert)

玩家执行一个额外的回合
支持参数：
- skill：字符串，触发额外回合的技能id，用于记录和判断等，非必要
- insert：布尔值，是否插入到最前面，默认为false，表示插入到最后
```javascript
player.insertPhase('xxx'); //插入一个额外回合
```

### changeShiQi(num,side)

NoTrigger
触发器按顺序依次为
changeShiQiJudge
changeShiQiBefore
-改变，士气更新
changeShiQiEnd
changeShiQiAfter
改变某一方的士气
支持参数，支持手动set参数'shiQiMax'，用于设置增减上限
- num：数值，正数表示增加，负数表示减少，若无num参数，默认为1
- side：布尔值，若无side参数，则阵营为调用玩家阵营
```javascript
player.changeShiQi(2); //将我方士气+2
```

### changeZhanJi(xingShi,num,side)

改变某一方战绩区的星石数量
支持参数：
- xingShi：字符串，支持'baoShi'和'shuiJing'
- num：数值，若无num参数，默认为1
- side：布尔值，若无side参数，则阵营为调用玩家阵营
```javascript
player.changeZhanJi('baoShi',2); //将我方战绩区+2宝石
```

### addZhanJi(xingShi,num)

添加战绩区num个星石
支持参数：
- xingShi：字符串，支持'baoShi'和'shuiJing'
- num：数值，默认为1
```javascript
player.addZhanJi('shuiJing',2); //战绩区增加2个水晶
```

### removeZhanJi(xingShi,num)

移除战绩区num个星石
支持参数：
- xingShi：字符串，支持'baoShi'和'shuiJing'
- num：数值，默认为1
```javascript
player.removeZhanJi('shuiJing',1); //战绩区减少1个水晶
```

### changeXingBei(num,side)

改变某一方的星杯数
支持参数：
- num：数值，若无num参数，默认为1
- side：布尔值，若无side参数，则阵营为调用玩家阵营
```javascript
player.changeXingBei(1); //将我方星杯+1
```

### showCards(cards,str)

玩家展示卡牌，可触发封印师封印
支持参数：
- cards：卡牌列表
- str：字符串，str参数为自定义展示弹窗文字，若无str参数，则默认为"玩家名展示的牌"
```javascript
player.showCards(cards,'请注意这些牌');
```

### showHiddenCards(cards,str)

展示出隐藏卡牌，不触发封印师封印
支持参数：
- cards：卡牌列表
- str：字符串，str参数为自定义展示弹窗文字，若无str参数，则默认为"玩家名展示的牌"
```javascript
player.showHiddenCards(cards);
```

### removeBiShaShuiJing()

消耗一个水晶（通常写在需要消耗水晶的技能里），若玩家同时拥有水晶和宝石，则让玩家进行选择
```javascript
player.removeBiShaShuiJing();
```

### removeBiShaBaoShi()

消耗一个宝石，等价于removeNengLiang('baoShi',1)
```javascript
player.removeBiShaBaoShi();
```

### changeNengLiang(xingShi,num)

改变玩家能量数量
支持参数：
- xingShi：字符串，参数支持'baoShi'和'shuiJing'
- num：数值，可正可负，正数表示增加，负数表示减少，若无num参数，默认为1
```javascript
player.changeNengLiang('shuiJing',-1); //减少1个水晶
```

### addNengLiang(xingShi,num)

增加玩家能量
支持参数：
- xingShi：字符串，参数支持'baoShi'和'shuiJing'
- num：数值，默认为1
```javascript
player.addNengLiang('baoShi',2); //增加2个宝石
```

### removeNengLiang(xingShi,num)

移除玩家能量，xingShi参数支持'baoShi'和'shuiJing'，num参数默认为1
```javascript
player.removeNengLiang('shuiJing'); //移除1个水晶
```

### changeZhiShiWu()

改变指示物数量
支持参数：
- 数值1：改变数量，正数增加，负数减少，默认为1
- 数值2：改变过程中指示物上限，若无，则使用指示物默认上限
- 字符串：指示物id
- 布尔值：是否强制增减，默认false，若无对应指示物技能，则无法增减
```javascript
player.changeZhiShiWu('xxx',2,4);
//增加2个xxx，上限最多为4
```

### addZhiShiWu()

添加指示物数量
支持参数：
- 数值1：改变数量，正数增加，负数将转化为正数，默认为1
- 数值2：改变过程中指示物上限，若无，则使用指示物默认上限
- 字符串：指示物id
- 布尔值：是否强制增减，默认false，若无对应指示物技能，则无法增减
```javascript
player.addZhiShiWu('xxx');
//增加1个xxx
```

### removeZhiShiWu()

移除指示物
支持参数：
- 数值1：减少数量，正数减少，默认为1
- 字符串：指示物id
```javascript
player.removeZhiShiWu('xxx');
//减少1个xxx
```

### setZhiShiWu(zhiShiWu, num)

将指示物设置为num个，不会突破上限，可set('max',num)来设置上限
支持参数：
- 字符串：指示物id
- 数值：数量
```javascript
player.setZhiShiWu('xxx',3);
//将xxx设置为3个
```


### changeHong(num,max)

用于技能效果中，便捷改变红色指示物数量
支持参数：
- num：数值，正数表示增加，负数表示减少，若无num参数，默认为1
- max：数值，指示物上限，若无，则使用指示物默认上限
```javascript
player.changeHong(2,5);
```

### changeLan(num,max)

用于技能效果中，便捷改变蓝色指示物数量
支持参数：
- num：数值，正数表示增加，负数表示减少，若无num参数，默认为1
- max：数值，指示物上限，若无，则使用指示物默认上限
```javascript
player.changeLan(-1);
```

### addHong(num,max)

用于技能效果中，便捷增加红色指示物数量
支持参数：
- num：数值，默认为1
- max：数值，指示物上限，若无，则使用指示物默认上限
```javascript
player.addHong(3,5);
```

### addLan(num,max)

用于技能效果中，便捷增加蓝色指示物数量
支持参数：
- num：数值，默认为1
- max：数值，指示物上限，若无，则使用指示物默认上限
```javascript
player.addLan(2,4);
```

### removeHong(num)

用于技能效果中，便捷移除红色指示物数量
支持参数：
- num：数值，默认为1
```javascript
player.removeHong(1);
```

### removeLan(num)

用于技能效果中，便捷移除蓝色指示物数量
支持参数：
- num：数值，默认为1
```javascript
player.removeLan(2);
```

### chongZhi()

将角色重置（通常用于退形态）
```javascript
player.chongZhi();
```

### hengZhi()

将角色横置（通常用于进形态）
```javascript
player.hengZhi();
```

### qiPai()

角色执行弃牌，执行一次超出手牌上限的弃牌，若手牌未超出上限，则不执行弃牌
用于部分手牌上限下降的技能，来触发弃牌，现检测检测实际较为完善，非必要无需使用
```javascript
player.qiPai();
```

### changeZhiLiao()

修改角色的治疗数
支持参数：
- 数值1：正数表示增加，负数表示减少，若无num参数，默认为1
- 数值2：改变过程中治疗上限，若无，则使用角色默认上限
- 玩家：治疗来源，默认无
```javascript
player.changeZhiLiao(1,3);
//角色治疗+1，治疗最多为3
```

### addZhiLiao(num,limit)

角色添加num个治疗
支持参数：
- num：数值，默认为1
- limit：数值，治疗上限，若无，则使用角色默认上限
```javascript
player.addZhiLiao(2);
```

### removeZhiLiao(num)

角色移除num个治疗
支持参数：
- num：数值，默认为1
```javascript
player.removeZhiLiao(1);
```

### addFengYin(fengYin,cards,source)

为角色添加封印
支持参数：
- fengYin：字符串，封印id
- cards：卡牌列表，作为封印的卡牌
- source：玩家，封印来源
```javascript
player.addFengYin('huoZhiFengYin_xiaoGuo', cards, player);
```

### changeSkills(addSkill = [], removeSkill = [], popup = true)

玩家替换技能
支持参数：
- addSkill：列表，添加的技能列表
- removeSkill：列表，移除的技能列表
- popup：布尔值，是否弹出技能名，和发动技能时的弹出一致，默认为true
```javascript
player.changeSkills(['xxx'], ['yyy']);
```

### swapHandcards(target,cards1,cards2)

玩家与target交换牌
支持参数：
- target：交换手牌的目标玩家
- cards1：玩家选择交换的牌列表，若未设置，则为全部手牌
- cards2：目标玩家选择交换的牌列表，若未设置，则为全部手牌
```javascript
player.swapHandcards(targetPlayer);
```

### chooseToUse(use)

玩家选择使用卡牌，无技能使用

### moDan(use)

NoTrigger
让角色使用魔弹，无技能调用

### yingZhan(use)

让角色进行应战攻击，阴阳师代替应战中使用，无其他技能调用

### gongJiOrFaShu(use)

NoTrigger
让角色进行攻击或者法术行动

### gongJi(use)

NoTrigger
让角色进行攻击行动

### faShu(use)

NoTrigger
让角色进行法术行动

### qiTa(use)

让角色进行其他行动，无技能调用