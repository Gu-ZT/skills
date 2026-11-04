# 单元测试与 GameTest

ModDevGradle（MDG）支持使用 JUnit 5 对模组逻辑编写单元测试，并可在测试代码中直接引用 Minecraft 与 NeoForge 类。

## `build.gradle` 单元测试配置

```groovy
dependencies {
    // 版本号需根据模板仓库或最新查询结果填写，禁止直接照抄示例值
    testImplementation 'org.junit.jupiter:junit-jupiter:5.10.2'
    testRuntimeOnly 'org.junit.platform:junit-platform-launcher'
}

test {
    useJUnitPlatform()
}

neoForge {
    unitTest {
        enable()
        testedMod = mods."${mod_id}" // 绑定当前被测模组
    }
}
```

## 服务端环境测试（`testframework`）

当测试逻辑依赖完整 `MinecraftServer` 实例时，引入 `testframework` 并配合 `@ExtendWith(EphemeralTestServerProvider.class)`：

```groovy
dependencies {
    testImplementation "net.neoforged:testframework:${neo_version}"
}
```

```java
@ExtendWith(EphemeralTestServerProvider.class)
public class ServerLogicTest {
    @Test
    public void testWithServer(MinecraftServer server) {
        // 在临时服务端上下文中执行验证
    }
}
```

## 执行命令

- 运行 JUnit 单元测试：`./gradlew test`
- 运行游戏内集成测试（GameTest）：`./gradlew runGameTestServer`
