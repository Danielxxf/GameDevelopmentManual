# 游戏设计模式（Game Programming Patterns）
游戏设计模式是一种用于解决游戏开发中的常见问题的设计模式，与软件开发中的常见设计模式类似，但是它们是特别针对游戏的需求而设计的。以下是使用游戏设计模式的一些原因：  
1. 使游戏更易于维护：游戏设计模式可以使游戏代码更有组织，更易于维护。在游戏开发过程中，开发者可能会面临许多复杂的需求和设计问题，游戏设计模式为这些问题提供了一些解决方案，使代码更易于调试和维护。  
2. 加速游戏开发：游戏设计模式可以提高游戏开发的效率。通过使用已经证明有效的设计模式，开发者可以更快地开发游戏，并且可以避免由于设计不良而导致的错误和代码冗余。  
3. 更好地组织游戏功能：游戏设计模式可以帮助开发者更好地组织游戏功能。通过将功能分成可重用的组件，开发者可以更轻松地在游戏中实现新功能。  
4. 提高游戏质量：使用游戏设计模式可以提高游戏的质量。游戏设计模式可以减少游戏中的错误和异常情况，并确保游戏在不同设备和操作系统上的兼容性。  



## 常见设计模式在 Unity 中的实现

[**https://github.com/TYJia/GameDesignPattern_U3D_Version**](https://github.com/TYJia/GameDesignPattern_U3D_Version)

### 单例模式（Singleton Pattern）

```csharp
public class GameManager : MonoBehaviour
{
    private static GameManager instance;

    private void Awake()
    {
        if (instance == null)
        {
            instance = this;
            DontDestroyOnLoad(gameObject);
        }
        else
        {
            Destroy(gameObject);
        }
    }

    public static GameManager GetInstance()
    {
        return instance;
    }
}
```

在上述代码中，GameManager是一个游戏管理器类，我们使用单例模式保证整个游戏中只存在一个GameManager实例。在Awake()函数中，我们判断GameManager实例是否为null，如果是，就表示这是第一次实例化GameManager，我们就将实例化后的GameManager设置为instance，并使用DontDestroyOnLoad()函数保证GameManager对象在场景切换时不会被摧毁。如果GameManager实例不为null，就直接销毁它。

### 工厂模式（Factory Pattern）

```csharp
public enum EnemyType
{
    Normal,
    Elite,
    Boss
}

public class EnemyFactory : MonoBehaviour
{
    public GameObject normalEnemyPrefab;
    public GameObject eliteEnemyPrefab;
    public GameObject bossEnemyPrefab;

    public GameObject CreateEnemy(EnemyType type)
    {
        GameObject enemy = null;
        switch (type)
        {
            case EnemyType.Normal:
                enemy = Instantiate(normalEnemyPrefab);
                break;
            case EnemyType.Elite:
                enemy = Instantiate(eliteEnemyPrefab);
                break;
            case EnemyType.Boss:
                enemy = Instantiate(bossEnemyPrefab);
                break;
            default:
                Debug.LogError("Unknown enemy type.");
                break;
        }
        return enemy;
    }
}
```

在上述代码中，EnemyFactory是一个敌人工厂类，它可以使用CreateEnemy()函数创建不同类型的敌人，根据传入的EnemyType参数选择不同的敌人预制体进行实例化。这样，在游戏中，我们只需要调用EnemyFactory的CreateEnemy()函数就可以创建不同类型的敌人了。

### 观察者模式（Observer Pattern）

```csharp
public class Player : MonoBehaviour
{
    public delegate void PlayerDeathHandler();
    public static event PlayerDeathHandler OnPlayerDeath;

    private void OnTriggerEnter(Collider other)
    {
        if (other.CompareTag("Enemy"))
        {
            Destroy(gameObject);
            if (OnPlayerDeath != null)
            {
                OnPlayerDeath();
            }
        }
    }
}

public class UIManager : MonoBehaviour
{
    private void Start()
    {
        Player.OnPlayerDeath += GameOver;
    }

    private void GameOver()
    {
        Debug.Log("Game Over!");
    }
}
```

在上述代码中，Player是一个玩家类，它有一个OnPlayerDeath事件，当玩家死亡时，就会触发OnPlayerDeath事件。UIManager是一个UI管理器类，在Start()函数中，它注册了OnPlayerDeath事件的监听，当OnPlayerDeath事件被触发时，就会调用GameOver()函数来显示游戏结束的UI。

### 策略模式（Strategy Pattern）

```csharp
public interface IMoveStrategy
{
    void Move
    (Transform transform);
}

public class MoveForwardStrategy : IMoveStrategy
{
    public void Move(Transform transform)
    {
        transform.Translate(Vector3.forward * Time.deltaTime);
    }
}

public class MoveBackwardStrategy : IMoveStrategy
{
    public void Move(Transform transform)
    {
        transform.Translate(Vector3.back * Time.deltaTime);
    }
}

public class MoveLeftStrategy : IMoveStrategy
{
    public void Move(Transform transform)
    {
        transform.Translate(Vector3.left * Time.deltaTime);
    }
}

public class MoveRightStrategy : IMoveStrategy
{
    public void Move(Transform transform)
    {
        transform.Translate(Vector3.right * Time.deltaTime);
    }
}

public class MoveController : MonoBehaviour
{
    private IMoveStrategy moveStrategy;

    public void SetMoveStrategy(IMoveStrategy strategy)
    {
        moveStrategy = strategy;
    }

    public void Move()
    {
        if (moveStrategy != null)
        {
            moveStrategy.Move(transform);
        }
    }
}
```

### 命令模式（Command Pattern）

```csharp
public interface ICommand
{
    void Execute();
}

public class JumpCommand : ICommand
{
    private Rigidbody rigidbody;
    private float jumpForce;

    public JumpCommand(Rigidbody rb, float force)
    {
        rigidbody = rb;
        jumpForce = force;
    }

    public void Execute()
    {
        rigidbody.AddForce(Vector3.up * jumpForce, ForceMode.Impulse);
    }
}

public class InputHandler : MonoBehaviour
{
    private ICommand jumpCommand;

    private void Update()
    {
        if (Input.GetKeyDown(KeyCode.Space))
        {
            ExecuteCommand(jumpCommand);
        }
    }

    public void SetJumpCommand(ICommand command)
    {
        jumpCommand = command;
    }

    private void ExecuteCommand(ICommand command)
    {
        if (command != null)
        {
            command.Execute();
        }
    }
}
```

在上述代码中，ICommand是一个命令接口，它定义了Execute()函数，不同的命令类（JumpCommand）实现了不同的命令功能。InputHandler是一个输入处理器类，它包含了一个ICommand成员变量和一个SetJumpCommand()函数，通过SetJumpCommand()函数设置命令，当玩家按下空格键时，ExecuteCommand()函数会将命令执行。

以上就是五种常用设计模式的示例代码，它们在Unity中的应用非常广泛，并可以帮助开发者更好地管理代码和资源，提高游戏的可维护性、可扩展性和可读性。
