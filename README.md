# UnityFPSUnlocker
[README_JP](https://github.com/hexstr/UnityFPSUnlocker/blob/zygisk_module/README_jp.md)

## 安装需求
- [Magisk](https://github.com/topjohnwu/Magisk/releases)
- 启用`zygisk`

## 使用
下载并刷入模块。在重启之前，先下载`TargetList.json`放入`/data/local/tmp/TargetList.json`，并修改你的配置。  
插件会通过判断是否存在`/sdcard/Android/data/{package_name}/files/il2cpp`来自动加载。

```
{
  "global": {
    "delay": 10,
    "mod_opcode": true,
    "fps": 90,
    "scale": 1.0
  },
  "custom": {
    "com.random.package.name.a": {
      "fps": 60
    },
    "com.random.package.name.b": {
      "mod_opcode": false
    },
    "com.random.package.name.c": {
      "delay": 5
    }
  }
}
```

其中，`global`节点中的配置为:

- `fps` 需要设置的`fps`，设置为`0`以禁用
- `delay` 游戏载入后等待`delay`秒执行
- `mod_opcode` 是否修改`opcode`，如果你发现游戏会重新锁定fps，可以把这项改为`true`，但由于修改内存，可能会被反作弊检测到
- `scale` 设置分辨率的倍数，一般保持`1.0`即可，必须为小数。`当前屏幕宽度 * scale x 当前屏幕高度 * scale`

然后，`custom`节点中的配置会覆盖`global`中的配置单独生效:

- `key` 包名，比如`com.random.package.name.a`
- `fps` 同上
- `mod_opcode` 同上
- `delay` 同上
- `scale` 同上

`TargetList.json`修改后可以搜索`json 格式校验`校验是否完整。修改后立即生效（`模块版本>=1.8`）。  
可以在终端模拟器输入`logcat -s UnityFPSUnlocker`查看输入日志。

## 分辨率
最近发现`BlueArchive`最高分辨率只有`1080P`，在模拟器上有肉眼可见的锯齿，而且在`16:10`的比例下甚至像素点比`16:9`更少

`2560x1600->1822x1138`

对比

`2560x1440->1920x1080`

所以加上调整分辨率的功能，对比图如下

https://imgsli.com/MjI3NDQ2/0/1

https://imgsli.com/MjI3NDQ2/2/3

但是设置的时机需要尽可能早，也就是`delay`尽可能短，否则需要更改`绘图`选项中的任意一项后生效（比如开关一次`抗锯齿`）

如果你不需要超分辨率，可以修改`/sdcard/Android/data/com.nexon.bluearchive/files/DeviceOption`，把`Resolution`修改为大于`3`即可，这样会走`default`分支(在函数`GraphicsManager.CoSetScreenResolution()`中)

- `0`: 1080P
- `1`: 720P
- `2`: 540P
- `3`: 480P
- `default` default


## 설치 요구사항
- [마기스크](https://github.com/topjohnwu/Magisk/releases)
- `zygisk` 활성화

## 사용
모듈을 다운로드하고 플래시하세요. 다시 시작하기 전에 `TargetList.json`을 `/data/local/tmp/TargetList.json`에 다운로드하고 구성을 수정하세요.  
플러그인이 존재하는지 여부를 확인합니다.


```
{
  "global": {
    "delay": 10,
    "mod_opcode": true,
    "fps": 90,
    "scale": 1.0
  },
  "custom": {
    "com.random.package.name.a": {
      "fps": 60
    },
    "com.random.package.name.b": {
      "mod_opcode": false
    },
    "com.random.package.name.c": {
      "delay": 5
    }
  }
}
```

그중 `global` 노드의 구성은 다음과 같습니다.

- `fps` `fps`를 설정하고 `0`으로 설정하여 비활성화합니다.
- `delay`는 게임이 로드된 후 `delay` 초 동안 실행될 때까지 기다립니다.
- `mod_opcode` `opcode` 수정 여부, 게임이 fps를 다시 잠그는 것으로 확인되면 이를 `true`로 변경할 수 있지만, 메모리 수정으로 인해 부정행위 방지에 의해 감지될 수 있습니다.
- `scale`은 해상도의 배수를 설정하며 일반적으로 소수점 이하 `1.0`으로 유지됩니다. `현재 화면 너비 * 배율 x 현재 화면 높이 * 배율`

그러면 `custom` 노드의 구성이 `global`의 구성을 재정의하고 별도로 적용됩니다.

- `com.random.package.name.a`와 같은 `key` 패키지 이름
- `fps` 위와 동일
- `mod_opcode` 위와 동일
- `delay` 위와 동일
- `scale` 위와 동일

`TargetList.json`을 수정한 후 `json 형식 확인`을 검색하여 완료되었는지 확인할 수 있습니다. 수정 사항은 즉시 적용됩니다(`모듈 버전>=1.8`).  
터미널 에뮬레이터에 `logcat -s UnityFPSUnlocker`를 입력하면 입력 로그를 볼 수 있습니다.

## 해결
최근 'BlueArchive'의 최고 해상도는 '1080P'에 불과하고 시뮬레이터에 눈에 띄는 별칭이 있으며 '16:10' 비율에서는 '16:9'보다 픽셀 수가 훨씬 적은 것으로 나타났습니다.

`2560x1600->1822x1138`

차이

`2560x1440->1920x1080`

따라서 해상도 조정 기능에 따른 비교표는 다음과 같습니다.

https://imgsli.com/MjI3NDQ2/0/1

https://imgsli.com/MjI3NDQ2/2/3

그러나 설정 시간은 최대한 빨라야 합니다. 즉, 지연 시간이 최대한 짧아야 합니다. 그렇지 않으면 그리기 옵션을 변경해야 적용됩니다(예: 앤티앨리어싱을 한 번 켜는 것).

초해상도가 필요하지 않은 경우 `/sdcard/Android/data/com.nexon.bluearchive/files/DeviceOption`을 수정하고 `해상도`를 `3`보다 크게 변경할 수 있습니다. 이렇게 하면 `기본값'이 사용됩니다. ` 분기(`GraphicsManager.CoSetScreenResolution()` 함수에서)

- '0': 1080P
- '1': 720P
-`2`: 540P
- `3`: 480P
- `기본` 기본값
