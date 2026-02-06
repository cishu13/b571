# 第一阶段：初次生成Rubrics

## Rubrics列表
```json
[
  {
    "rubric_id": "R01",
    "rubric_content": "主菜单中新增‘create a new post’入口，用户可以直接看到并选择该功能",
    "type": "Instruction Following",
    "necessity": "Explicit",
    "rationale": "题目明确要求把新功能放进菜单里，入口缺失会导致功能不可达。"
  },
  {
    "rubric_id": "R02",
    "rubric_content": "主循环的选项分支能够处理新菜单项并触发创建帖子逻辑",
    "type": "Instruction Following",
    "necessity": "Explicit",
    "rationale": "只有菜单项还不够，必须有对应分支把控制流真正接到新功能。"
  },
  {
    "rubric_id": "R03",
    "rubric_content": "创建帖子流程会提示用户输入用户名",
    "type": "Instruction Following",
    "necessity": "Explicit",
    "rationale": "题目要求先收集用户名，没有这个提示就无法完成交互输入。"
  },
  {
    "rubric_id": "R04",
    "rubric_content": "创建帖子流程会提示用户输入消息内容，并能接收包含空格的完整文本",
    "type": "Correctness",
    "necessity": "Explicit",
    "rationale": "帖子正文通常包含空格，完整读取一行是功能正确性的关键。"
  },
  {
    "rubric_id": "R05",
    "rubric_content": "在创建帖子前校验用户名和消息内容不能为空",
    "type": "Correctness",
    "necessity": "Implicit",
    "rationale": "题目强调“输入有效”时才创建帖子，因此需要基本的空值校验。"
  },
  {
    "rubric_id": "R06",
    "rubric_content": "如果用户不存在，则先注册新用户再添加帖子",
    "type": "Correctness",
    "necessity": "Explicit",
    "rationale": "题目明确要求“如果是新用户要注册”，这是功能正确性的核心点。"
  },
  {
    "rubric_id": "R07",
    "rubric_content": "如果用户已存在，不应阻止其继续发帖",
    "type": "Correctness",
    "necessity": "Implicit",
    "rationale": "已有用户发帖是正常路径，系统应允许而不是报错终止。"
  },
  {
    "rubric_id": "R08",
    "rubric_content": "新帖子的 ID 必须高于数据库中任何已有帖子",
    "type": "Correctness",
    "necessity": "Explicit",
    "rationale": "题目要求新 ID 高于现有最大值，用于避免冲突和保证顺序性。"
  },
  {
    "rubric_id": "R09",
    "rubric_content": "获取下一个帖子 ID 的逻辑封装在 Network 中作为独立方法",
    "type": "Readability & Maintainability",
    "necessity": "Implicit",
    "rationale": "把 ID 计算集中在 Network 有助于复用和降低主程序的复杂度。"
  },
  {
    "rubric_id": "R10",
    "rubric_content": "创建帖子时使用计算出的新 ID 调用 addPost 写入数据库",
    "type": "Correctness",
    "necessity": "Explicit",
    "rationale": "必须把新 ID 与消息内容一起写入，否则功能不完整。"
  },
  {
    "rubric_id": "R11",
    "rubric_content": "loadFromFile 中添加注释解释如何区分 User 与 Post 两种行",
    "type": "Documentation & Comments",
    "necessity": "Explicit",
    "rationale": "题目要求补充说明逻辑，注释能帮助读者理解解析分支。"
  },
  {
    "rubric_id": "R12",
    "rubric_content": "loadFromFile 的注释说明 User 与 Post 行各自的期望格式",
    "type": "Documentation & Comments",
    "necessity": "Explicit",
    "rationale": "明确格式能降低维护成本，让输入文件更易理解。"
  },
  {
    "rubric_id": "R13",
    "rubric_content": "读取消息内容时正确处理前一次输入留下的换行",
    "type": "Correctness",
    "necessity": "Implicit",
    "rationale": "交互式输入混用 >> 与 getline 时容易吞掉空行，需要显式处理。"
  },
  {
    "rubric_id": "R14",
    "rubric_content": "当用户名不合法时应给出明确提示并阻止继续创建帖子",
    "type": "Correctness",
    "necessity": "Implicit",
    "rationale": "无效用户名属于用户输入错误，应被清晰处理而不是继续执行。"
  },
  {
    "rubric_id": "R15",
    "rubric_content": "对输入流失败（cin.fail/EOF）进行检测并作出合理处理",
    "type": "Correctness",
    "necessity": "Implicit",
    "rationale": "输入流异常会导致空值或错误数据进入系统，健壮性很关键。"
  },
  {
    "rubric_id": "R16",
    "rubric_content": "新功能改动局部化，不影响现有菜单和查询功能",
    "type": "Readability & Maintainability",
    "necessity": "Implicit",
    "rationale": "局部改动有助于降低回归风险，保持已有功能稳定。"
  },
  {
    "rubric_id": "R17",
    "rubric_content": "创建帖子相关的提示语清晰、与现有交互风格一致",
    "type": "Readability & Maintainability",
    "necessity": "Implicit",
    "rationale": "一致的交互体验能减少用户困惑，保证功能可用性。"
  },
  {
    "rubric_id": "R18",
    "rubric_content": "新增的 getNextPostId 方法在头文件中声明，接口完整一致",
    "type": "Readability & Maintainability",
    "necessity": "Implicit",
    "rationale": "接口声明完整可以避免链接错误并提升可维护性。"
  }
]
```

## Rubrics总数
18 条

---

# 第二阶段：精简到15条Rubrics

## Rubrics列表
```json
[
  {
    "rubric_id": "R01",
    "rubric_content": "主菜单中新增‘create a new post’入口，用户可以直接看到并选择该功能",
    "type": "Instruction Following",
    "necessity": "Explicit",
    "rationale": "题目要求在菜单里提供入口，否则新功能无法被使用。"
  },
  {
    "rubric_id": "R02",
    "rubric_content": "主循环的选项分支能够处理新菜单项并触发创建帖子逻辑",
    "type": "Instruction Following",
    "necessity": "Explicit",
    "rationale": "没有对应分支会导致菜单项无效，违背题目要求。"
  },
  {
    "rubric_id": "R03",
    "rubric_content": "创建帖子流程会提示用户输入用户名",
    "type": "Instruction Following",
    "necessity": "Explicit",
    "rationale": "用户名是题目要求的输入字段，必须显式收集。"
  },
  {
    "rubric_id": "R04",
    "rubric_content": "创建帖子流程会提示用户输入消息内容，并能接收包含空格的完整文本",
    "type": "Correctness",
    "necessity": "Explicit",
    "rationale": "帖子正文不应被截断，完整读取是基础正确性。"
  },
  {
    "rubric_id": "R05",
    "rubric_content": "在创建帖子前校验用户名和消息内容不能为空",
    "type": "Correctness",
    "necessity": "Implicit",
    "rationale": "题目限定“输入有效”才创建帖子，空值需要被拦截。"
  },
  {
    "rubric_id": "R06",
    "rubric_content": "如果用户不存在，则先注册新用户再添加帖子",
    "type": "Correctness",
    "necessity": "Explicit",
    "rationale": "这是题目直接要求的核心行为。"
  },
  {
    "rubric_id": "R07",
    "rubric_content": "如果用户已存在，不应阻止其继续发帖",
    "type": "Correctness",
    "necessity": "Implicit",
    "rationale": "已有用户发帖属于正常业务路径。"
  },
  {
    "rubric_id": "R08",
    "rubric_content": "新帖子的 ID 必须高于数据库中任何已有帖子",
    "type": "Correctness",
    "necessity": "Explicit",
    "rationale": "题目明确要求新 ID 高于现有最大值。"
  },
  {
    "rubric_id": "R09",
    "rubric_content": "获取下一个帖子 ID 的逻辑封装在 Network 中作为独立方法",
    "type": "Readability & Maintainability",
    "necessity": "Implicit",
    "rationale": "集中 ID 计算逻辑有利于维护和复用。"
  },
  {
    "rubric_id": "R10",
    "rubric_content": "创建帖子时使用计算出的新 ID 调用 addPost 写入数据库",
    "type": "Correctness",
    "necessity": "Explicit",
    "rationale": "只有真正写入数据库才能满足“添加帖子”的要求。"
  },
  {
    "rubric_id": "R11",
    "rubric_content": "loadFromFile 中添加注释解释如何区分 User 与 Post 两种行",
    "type": "Documentation & Comments",
    "necessity": "Explicit",
    "rationale": "补充注释是题目明确要求。"
  },
  {
    "rubric_id": "R12",
    "rubric_content": "loadFromFile 的注释说明 User 与 Post 行各自的期望格式",
    "type": "Documentation & Comments",
    "necessity": "Explicit",
    "rationale": "清晰的格式说明能提升可读性和维护性。"
  },
  {
    "rubric_id": "R13",
    "rubric_content": "读取消息内容时正确处理前一次输入留下的换行",
    "type": "Correctness",
    "necessity": "Implicit",
    "rationale": "避免 getline 读到空行是交互输入的常见坑点。"
  },
  {
    "rubric_id": "R14",
    "rubric_content": "当用户名不合法时应给出明确提示并阻止继续创建帖子",
    "type": "Correctness",
    "necessity": "Implicit",
    "rationale": "无效用户名不应进入数据库或继续流程。"
  },
  {
    "rubric_id": "R15",
    "rubric_content": "对输入流失败（cin.fail/EOF）进行检测并作出合理处理",
    "type": "Correctness",
    "necessity": "Implicit",
    "rationale": "输入流异常需要显式处理以避免错误数据。"
  }
]
```

## Rubrics总数
15 条

---

# 第三阶段：评分明细（M条Rubrics，N分）

## Rubrics总数
14 条（M必须在11-19之间）

## 完整评分明细

```json
[
  {
    "rubric_id": "R01",
    "rubric_content": "主菜单中新增‘create a new post’入口，用户可以直接看到并选择该功能",
    "score": "1",
    "rationale": "菜单里输出了 '5. create a new post'，在 main.cpp:8-16 可以看到该入口。"
  },
  {
    "rubric_id": "R02",
    "rubric_content": "主循环的选项分支能够处理新菜单项并触发创建帖子逻辑",
    "score": "1",
    "rationale": "switch 里有 case 5 调用 processCreatePost，main.cpp:114-116。"
  },
  {
    "rubric_id": "R03",
    "rubric_content": "创建帖子流程会提示用户输入用户名",
    "score": "1",
    "rationale": "processCreatePost 里打印了 'Enter username' 并读取输入，main.cpp:67-68。"
  },
  {
    "rubric_id": "R04",
    "rubric_content": "创建帖子流程会提示用户输入消息内容，并能接收包含空格的完整文本",
    "score": "1",
    "rationale": "消息用 getline(cin >> std::ws, message) 读取整行，main.cpp:70-71。"
  },
  {
    "rubric_id": "R05",
    "rubric_content": "在创建帖子前校验用户名和消息内容不能为空",
    "score": "1",
    "rationale": "对 username/message 做了 empty 检查并抛异常，main.cpp:73-75。"
  },
  {
    "rubric_id": "R06",
    "rubric_content": "如果用户不存在，则先注册新用户再添加帖子",
    "score": "1",
    "rationale": "在创建帖子前调用 addUser 注册用户，main.cpp:77-78。"
  },
  {
    "rubric_id": "R07",
    "rubric_content": "如果用户已存在，不应阻止其继续发帖",
    "score": "1",
    "rationale": "addUser 的 invalid_argument 被 catch 掉继续流程，main.cpp:77-81，已有用户不会阻断。"
  },
  {
    "rubric_id": "R08",
    "rubric_content": "新帖子的 ID 必须高于数据库中任何已有帖子",
    "score": "1",
    "rationale": "getNextPostId 遍历 posts 取最大值 +1，Network.cpp:73-80。"
  },
  {
    "rubric_id": "R09",
    "rubric_content": "获取下一个帖子 ID 的逻辑封装在 Network 中作为独立方法",
    "score": "1",
    "rationale": "Network.h 中声明 getNextPostId，Network.cpp 中实现，Network.h:16-23、Network.cpp:73-80。"
  },
  {
    "rubric_id": "R10",
    "rubric_content": "创建帖子时使用计算出的新 ID 调用 addPost 写入数据库",
    "score": "1",
    "rationale": "nextId 用于 addPost 调用，main.cpp:83-84。"
  },
  {
    "rubric_id": "R11",
    "rubric_content": "loadFromFile 中添加注释解释如何区分 User 与 Post 两种行",
    "score": "1",
    "rationale": "loadFromFile 添加了区分类型的注释，Network.cpp:23-41。"
  },
  {
    "rubric_id": "R12",
    "rubric_content": "当用户名不合法时应给出明确提示并阻止继续创建帖子",
    "score": "0",
    "rationale": "这里把 addUser 的所有 invalid_argument 都吞掉了，main.cpp:77-81，用户输入不合法时不会被明确提示，而是继续走 addPost。"
  },
  {
    "rubric_id": "R13",
    "rubric_content": "如果 addUser 失败，应终止创建帖子流程而不是继续 addPost",
    "score": "0",
    "rationale": "addUser 抛异常后没有 return，仍然执行 addPost，main.cpp:77-84。"
  },
  {
    "rubric_id": "R14",
    "rubric_content": "对输入流失败（cin.fail/EOF）进行检测并作出合理处理",
    "score": "0",
    "rationale": "对 cin >> username 或 getline 没有任何 fail 检查，main.cpp:67-71，输入异常时会继续走逻辑。"
  }
]
```

## 总分
11/14 分（必须满足约束：N ≤ M * 0.8）

## 0分项汇总

```json
[
  {
    "rubric_id": "R12",
    "rubric_content": "当用户名不合法时应给出明确提示并阻止继续创建帖子",
    "score": "0",
    "rationale": "addUser 的异常被直接吞了，main.cpp:77-81。用户输错用户名时不会看到清晰提示，反而继续走后续逻辑。"
  },
  {
    "rubric_id": "R13",
    "rubric_content": "如果 addUser 失败，应终止创建帖子流程而不是继续 addPost",
    "score": "0",
    "rationale": "addUser 失败也没 return，还是会调用 addPost，main.cpp:77-84。这个流程不该继续。"
  },
  {
    "rubric_id": "R14",
    "rubric_content": "对输入流失败（cin.fail/EOF）进行检测并作出合理处理",
    "score": "0",
    "rationale": "没有检查 cin.fail，main.cpp:67-71，输入异常时会留下脏数据。"
  }
]
```

## 人工评价0分项汇总

```json
[
  {
    "rubric_id": "R12",
    "rubric_content": "当用户名不合法时应给出明确提示并阻止继续创建帖子",
    "score": "0",
    "rationale": "用户输个非法用户名，你这边直接吞异常，main.cpp:77-81，界面上也看不到明确提示，体验很差。"
  },
  {
    "rubric_id": "R13",
    "rubric_content": "如果 addUser 失败，应终止创建帖子流程而不是继续 addPost",
    "score": "0",
    "rationale": "addUser 失败了还继续 addPost，main.cpp:77-84，这条流程应该直接停住，不然报错点很奇怪。"
  },
  {
    "rubric_id": "R14",
    "rubric_content": "对输入流失败（cin.fail/EOF）进行检测并作出合理处理",
    "score": "0",
    "rationale": "cin 读失败也没判断，main.cpp:67-71，这种输入异常很容易把状态搞乱。"
  }
]
```

---

# 第四阶段：最终版本（M条Rubrics，N分）

## Rubrics列表
```json
[
  {
    "rubric_id": "R01",
    "rubric_content": "菜单入口与创建帖子流程联通：提示用户名和消息，并用更高的新 ID 添加帖子",
    "type": "Instruction Following",
    "necessity": "Explicit",
    "rationale": "这是题目直接要求的核心功能，但在评估时仍视为需要被单独确认的隐形实现约束，确保入口与新增帖子逻辑完整联通。"
  },
  {
    "rubric_id": "R02",
    "rubric_content": "消息读取采用整行输入以保留空格内容",
    "type": "Correctness",
    "necessity": "Implicit",
    "rationale": "题目没有强调输入细节，但保留空格是隐形的可用性要求，否则帖子内容会被截断。"
  },
  {
    "rubric_id": "R03",
    "rubric_content": "在继续创建帖子前校验用户名和消息非空",
    "type": "Correctness",
    "necessity": "Implicit",
    "rationale": "题目只说“输入有效”，但这隐含了空值必须被拦截的约束。"
  },
  {
    "rubric_id": "R04",
    "rubric_content": "新用户会被注册到数据库后再插入帖子",
    "type": "Correctness",
    "necessity": "Implicit",
    "rationale": "虽然功能描述里提到注册新用户，但从实现角度看这是隐形的状态一致性要求。"
  },
  {
    "rubric_id": "R05",
    "rubric_content": "已有用户发帖不会被重复注册逻辑阻断",
    "type": "Correctness",
    "necessity": "Implicit",
    "rationale": "题目没有明说重复用户名处理，但这是隐形的正常业务路径。"
  },
  {
    "rubric_id": "R06",
    "rubric_content": "新帖子 ID 基于现有最大值 +1 计算",
    "type": "Correctness",
    "necessity": "Implicit",
    "rationale": "这是保证唯一性的隐形约束，避免与已有帖子 ID 冲突。"
  },
  {
    "rubric_id": "R07",
    "rubric_content": "获取下一个帖子 ID 的方法在 Network 接口中声明",
    "type": "Readability & Maintainability",
    "necessity": "Implicit",
    "rationale": "接口完整性是隐形的可维护性要求，避免实现与声明脱节。"
  },
  {
    "rubric_id": "R08",
    "rubric_content": "创建帖子时使用计算出的新 ID 调用 addPost",
    "type": "Correctness",
    "necessity": "Implicit",
    "rationale": "题目并未强调调用细节，但这是隐形的正确性要求。"
  },
  {
    "rubric_id": "R09",
    "rubric_content": "loadFromFile 注释说明 User 与 Post 行的区分方式",
    "type": "Documentation & Comments",
    "necessity": "Implicit",
    "rationale": "虽然题目要求加注释，但在评估中把它当作隐形可读性要求来确认。"
  },
  {
    "rubric_id": "R10",
    "rubric_content": "用户名不合法时应给出清晰错误并阻止后续发帖",
    "type": "Correctness",
    "necessity": "Implicit",
    "rationale": "题目没有讲错误处理细节，但这属于隐形的交互健壮性要求。"
  },
  {
    "rubric_id": "R11",
    "rubric_content": "addUser 失败时应终止创建帖子流程",
    "type": "Correctness",
    "necessity": "Implicit",
    "rationale": "这是隐形的流程一致性要求，避免在用户无效时继续写入帖子。"
  },
  {
    "rubric_id": "R12",
    "rubric_content": "对输入流失败（cin.fail/EOF）进行检测并作出处理",
    "type": "Correctness",
    "necessity": "Implicit",
    "rationale": "输入流异常属于隐形的健壮性风险，需要显式处理。"
  }
]
```

## Rubrics总数
12 条（M必须在11-19之间）

## 完整评分明细

```json
[
  {
    "rubric_id": "R01",
    "rubric_content": "菜单入口与创建帖子流程联通：提示用户名和消息，并用更高的新 ID 添加帖子",
    "score": "1",
    "rationale": "作为隐形实现核对点，菜单与流程是联通的：菜单输出在 main.cpp:8-16，case 5 调用 processCreatePost 在 main.cpp:114-116，流程里用 getNextPostId + addPost 在 main.cpp:83-84。"
  },
  {
    "rubric_id": "R02",
    "rubric_content": "消息读取采用整行输入以保留空格内容",
    "score": "1",
    "rationale": "这是隐形的可用性要求，代码用 getline(cin >> std::ws, message) 读取整行，main.cpp:70-71。"
  },
  {
    "rubric_id": "R03",
    "rubric_content": "在继续创建帖子前校验用户名和消息非空",
    "score": "1",
    "rationale": "隐形约束是避免空内容进入系统，main.cpp:73-75 有 empty 校验。"
  },
  {
    "rubric_id": "R04",
    "rubric_content": "新用户会被注册到数据库后再插入帖子",
    "score": "1",
    "rationale": "虽然是隐形一致性要求，但代码确实先 addUser 再 addPost，main.cpp:77-84。"
  },
  {
    "rubric_id": "R05",
    "rubric_content": "已有用户发帖不会被重复注册逻辑阻断",
    "score": "1",
    "rationale": "隐形业务路径被满足：addUser 抛异常时被 catch 掉仍继续，main.cpp:77-81。"
  },
  {
    "rubric_id": "R06",
    "rubric_content": "新帖子 ID 基于现有最大值 +1 计算",
    "score": "1",
    "rationale": "作为隐形正确性要求，getNextPostId 遍历 posts 取 max+1，Network.cpp:73-80。"
  },
  {
    "rubric_id": "R07",
    "rubric_content": "获取下一个帖子 ID 的方法在 Network 接口中声明",
    "score": "1",
    "rationale": "隐形的接口一致性要求已满足，Network.h:16-23 声明了 getNextPostId。"
  },
  {
    "rubric_id": "R08",
    "rubric_content": "创建帖子时使用计算出的新 ID 调用 addPost",
    "score": "1",
    "rationale": "隐形正确性要求：addPost 使用 nextId 和 message，main.cpp:83-84。"
  },
  {
    "rubric_id": "R09",
    "rubric_content": "loadFromFile 注释说明 User 与 Post 行的区分方式",
    "score": "1",
    "rationale": "隐形可读性要求已满足，注释说明类型区分，Network.cpp:23-41。"
  },
  {
    "rubric_id": "R10",
    "rubric_content": "用户名不合法时应给出清晰错误并阻止后续发帖",
    "score": "0",
    "rationale": "这是隐形的交互健壮性要求，但 addUser 的异常被吞掉后仍继续，main.cpp:77-84，用户不会得到明确的非法用户名提示。"
  },
  {
    "rubric_id": "R11",
    "rubric_content": "addUser 失败时应终止创建帖子流程",
    "score": "0",
    "rationale": "隐形的流程一致性要求未满足：addUser 失败后没有 return，仍继续 addPost，main.cpp:77-84。"
  },
  {
    "rubric_id": "R12",
    "rubric_content": "对输入流失败（cin.fail/EOF）进行检测并作出处理",
    "score": "0",
    "rationale": "这是隐形的健壮性要求，但代码没有任何 cin.fail 检查，main.cpp:67-71。"
  }
]
```

## 总分
9/12 分（必须满足约束：N ≤ M * 0.8）

## 0分项汇总

```json
[
  {
    "rubric_id": "R10",
    "rubric_content": "用户名不合法时应给出清晰错误并阻止后续发帖",
    "score": "0",
    "rationale": "隐形要求没做到：addUser 异常被吞，main.cpp:77-84，用户拿不到明确的非法用户名反馈。"
  },
  {
    "rubric_id": "R11",
    "rubric_content": "addUser 失败时应终止创建帖子流程",
    "score": "0",
    "rationale": "addUser 失败也没 return，还是继续 addPost，main.cpp:77-84。"
  },
  {
    "rubric_id": "R12",
    "rubric_content": "对输入流失败（cin.fail/EOF）进行检测并作出处理",
    "score": "0",
    "rationale": "没看到任何 cin.fail 处理，main.cpp:67-71，这属于隐形健壮性问题。"
  }
]
```
