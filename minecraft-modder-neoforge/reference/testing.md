# 单元测试与 GameTest

MDG 支持通过 JUnit 对模组进行单元测试，测试中可引用 Minecraft 类。

## build.gradle 配置

```gradle
dependencies {
    testImplementation 'org.junit.jupiter:junit-jupiter:5.7.1'    // 示例版本，禁止照抄，以模板仓库或查询结果为准
    testRuntimeOnly 'org.junit.platform:junit-platform-launcher'
}

test {
    useJUnitPlatform()
}

neoForge {
    unitTest {
        enable()
        testedMod = mods."${mod_id}"    // 指定被测试的 mod
    }
}
```

## 加载服务端

测试需要服务端环境时引入 testframework：

```gradle
dependencies {
    testImplementation "net.neoforged:testframework:${neo_version}"
}
```

```java
@ExtendWith(EphemeralTestServerProvider.class)
public class TestClass {
    @Test
    public void testMethod(MinecraftServer server) {
        // 在服务端上下文中执行测试
    }
}
```

## 运行命令

- 单元测试：`./gradlew test`
- GameTest：`./gradlew runGameTestServer`
