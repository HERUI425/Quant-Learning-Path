# Quant-Learning-Path
Quantitative Finance Learning Path | 从数据准备到完整因子回测流水线
## Project Phases

### Phase 1: Robust Cross-Sectional Data Pipeline

开发了一个生产级的数据提取管道，基于 **Tushare API** 实现高效、稳定的金融数据获取。

**核心特性：**

- **反爬虫防御机制**：采用基于 `trade_cal` 日历的 **Calendar-Stepping Stepper**，系统性地规避高频请求封禁和速率限制。
- **张量对齐（Tensor Alignment）**：利用 Pandas `pivot_table` 的向量化操作，将非对称的交易日志转换为同步的、身份映射的二维截面矩阵  
  $\mathbf{X} \in \mathbb{R}^{T \times N}$，从根本上避免了前视偏差（look-ahead bias，如 `.shift(-1)`）。
- **数据规模**：已成功获取并处理 **21 天** 的高质量截面数据（日期范围：`[具体日期]`），为后续时序建模和因子研究奠定基础。

**技术亮点**：
- 完全向量化处理，性能优异
- 严格的时间对齐逻辑，确保矩阵每一列对应同一只股票、每一行对应同一交易日
- 生产级鲁棒性，可长期稳定运行
