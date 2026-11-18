# MagneticsDB2Inductor · 公开案例展示

**新增 [分钟级设计页](./fast.html)，2026-11-18 F3.2正式快照**：12例，完整外部63.79–87.72秒，2,069个数值候选，737个本轮完整组，2,004个组内三目标非支配候选；240代表/320工作点原核独立复核零差异。支持路线、完整组、复核层级、厂家/材料型号筛选，多工作点详情、未搜索/拒算说明和CSV/JSON/SVG导出。最多256提案、25%探索、单worker、120秒总时限；旧90%覆盖目标未达，物理认证未完成。

`fast.html`、`fast.css`、`fast.js`、`fast-data.js` 与共享样式一起部署；可直接本地打开，无外部请求。`scripts/build_fast_presentation.py`只从已验收F3.2五文件包导出白名单，`scripts/verify_fast_presentation.cjs`核对原值、组内支配关系与浏览器交互。本轮只做本地验收，未同步公开网页。

以下为保留的历史模式。独立静态网页，展示 2026-11-14 保存的 12 个 AC/DC 合成需求案例与真实数据库磁芯配置。

## 内容

- 12 案例 / 16 工作点切换，481 条案例短名单，其中 99 条全部工作点有数值。
- 案例讲解、厂家/材料/型号搜索、数值状态与完整比较签名筛选。
- 候选散点与详情联动，最多 3 个方案并列对照。
- 电流与恒 L 重建磁密的联动游标、多工作点结果矩阵。
- 可复制视图链接，导出当前方案 JSON 和筛选短名单 CSV。
- [全量数值候选优化散点图](./optimization.html)：18,459 个设计、694 个完整比较组、3,466 个组内三目标非支配候选；12 案例概览、厂家/材料着色、组筛选、体积/磁损上限、框选放大、候选详情和 CSV/JSON/SVG 导出。

## 运行与更新

网页无第三方依赖、字体/CDN 或后端请求，直接打开 index.html 或 optimization.html，或用任意静态服务器托管。部署目录包含 index.html、styles.css、app.js、data.js、optimization.html、optimization.css、optimization.js、optimization-data.js、.nojekyll 和本说明；数据库、PDF 与设计引擎源码不属于公开站点。优化数据单独加载，不增加原案例页的数据下载量。

私有源码工程中通过项目启动器运行 scripts/build_results_site.py，只读取并校验三份固定报告的 SHA-256，按明确字段清单输出 data.js。scripts/verify_results_site.cjs 检查浏览器交互。

scripts/build_optimization_scatter.py 流式读取已冻结 candidates.jsonl.gz，恢复 run.json 内保存的完整比较签名，复用已安装设计包的 screening_record / screen_records 输出 optimization-data.js；不执行新选型或损耗计算。scripts/verify_optimization_site.cjs 独立复核全部组的三目标支配关系并检查交互。

## 数值边界

电气输入是合成验证波形，结果不是样机实测。磁芯损耗为部分范围工程估算；偏磁、恒 L、温度与平台假设按方案显示。带载 L、饱和、绕组/铜损、总损耗、温升与机械加工未认证。

优化页的 18,459 个全点数值设计与案例页 99 条数值短名单属于不同口径。其余 207,708 个候选不完整，不绘为零。三目标 Pareto 仅在同一完整比较组内按 Ve、最坏 Pcore、N 判定，筛选不重算；不绘跨组统一前沿。批次 523 条回放由 481 条案例短名单与 42 条独立固定回归回放组成；后者未混入案例列表。每例 20,000 次有界试探已截断，不宣称全库最优。

数据来源哈希与详细假设在网页内可展开查看。源码仓库保持私有；本展示仓库只发布网页资源与筛选后的结果字段。
