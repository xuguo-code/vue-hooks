#### 分支规范

目前分支模式会采用类似`antd`的形式，分为`master`和`feat`两个主分支

- `master`分支

  1. 一些文档修复、bug 修复、项目底层能力比如打包修复会从`master`检出分支`fix/xxx`出来修复，修复完了通过`pr`合并回`master`

  2. 同时版本发布也会从`master`来检出

- `feat`分支

  开发新的 hooks 从 feat 检出分支`feature/xxx`，开发完成功能并且书写好相应文档和单元测试用例，通过`pr`的形式合并回`feat`

  最终包含新`hooks`的`feat`也会通过`pr`回归到`master`进行新版本的发布

- `release`分支

  `release/xxx`通常作为版本发布分支来做版本发布

#### 提交信息规范

- `commit`常规规范

  ```
  <类型>(作用域): 标题

  正文

  尾部
  ```

  > build：主要目的是修改项目构建系统(例如 glup，webpack，rollup 的配置等)的提交  
  > ci：主要目的是修改项目继续集成流程(例如 Travis，Jenkins，GitLab CI，Circle 等)的提交  
  > docs：文档更新  
  > feat：新增功能  
  > merge：分支合并 Merge branch ? of ?  
  > fix：bug 修复  
  > perf：性能, 体验优化  
  > refactor：重构代码(既没有新增功能，也没有修复 bug)  
  > style：不影响程序逻辑的代码修改(修改空白字符，格式缩进，补全缺失的分号等，没有改变代码逻辑)  
  > test：新增测试用例或是更新现有测试  
  > revert：回滚某个更早之前的提交  
  > chore：不属于以上类型的其他类型

- 保持提交信息的整洁

  > 上游分支：通常指你当前分支检出的来源分支，比如`master`
  >
  > 下游分支：通常指你当前开发功能或者修复`bug`的分支

  1. 下游分支同步上有分支必须采用`rebase`的形式，避免产生`merge commit`
  2. 下游分支开发中可灵活产生`WIP`开发中的中间`commit`信息，但是在最终申请合并到上游主分支前，需要`rebase -i`主分支并且通过`-i`来`fixup`不必要的`commit`信息，保持汇入主分支时`commit`信息的整洁

#### PR 相关

- `pr` 名称

`pr` 名称应当简介的概括当前 `pr` 所完成的事情，并且以分支名作为开始。

- `pr` 需要满足的 `CI` 条件

1. `Lint` 和 `test` 无报错
2. `doc build` 和 `bundle build` 无报错
3. `codecov` 不下降，并且当前功能的测试覆盖率在 `85%` 以上

- `pr` 包含的提交记录

最终的 `pr` 所包含的提交记录尽量不要包含中间状态的 `commit` 记录，比如：
如果是开发了一个新的 `hook` ，最终记录应该是线性的并且只包含 `feat(xxx): xxxx` 这样一条新增功能的有效 `commit`，
修复 `bug`也是相似的规则。
