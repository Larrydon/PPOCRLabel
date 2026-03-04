# 更新日誌

專案的版本更新內容會被記錄在這個檔案

更新日誌的格式將會基於 [Keep a Changelog](http://keepachangelog.com/en/1.0.0/)
==============================================================================
## [1.2.0] - 2026-03-04
### Changed
- `封掉 ReSize 320x48，恢復最原始的 get_rotate_crop_image() 僅裁切，什麼都不做，讓PaddleOCR 自己處理(yml[paddind: True])`


## [1.1.0] - 2026-03-03
### Changed
- `ReSize 改成 320x48 統一訓練集格式，針對台灣車牌優化:以車牌高度置中等比例縮放、寬度補齊padding(左右留空)`


## [1.0.0] - 2026-01-13
### Added
- `專案結構文件樹->RUN&FILETREE.md`
- `#原始碼src: Fork from [PPOCRLabel-v3.1.4](https://github.com/PFCCLab/PPOCRLabel/tree/v3.1.4)`


