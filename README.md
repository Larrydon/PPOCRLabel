# Fork from [PPOCRLabel-3.1.4](https://github.com/PFCCLab/PPOCRLabel)

資料參考來源:[【PaddleOCR-PPOCRLabel】标注工具使用](https://blog.csdn.net/z5z5z5z56/article/details/130238630)<br>
(docs\PaddleOCR-PPOCRLabel-CSDN-blog.csdn.net.mhtml)

Run ENV<br>
Python:3.9.25<br>
<br>

## 1. 完全清理
> pip uninstall paddlepaddle paddleocr paddlex PPOCRLabel numpy opencv-contrib-python opencv-python ultralytics torch torchvision torchaudio modelscope -y

> pip cache purge
<br>

## 2. 一次過安裝
> pip install -r requirements.txt --no-deps --no-cache-dir

>pip install -r requirements.txt  # 再跑一次解依賴
<br>

## 3. 安裝穩定 CPU PyTorch
> pip install torch==2.1.2 torchvision==0.16.2 torchaudio==2.1.2 --index-url https://download.pytorch.org/whl/cpu
<br>

## 4. 測試 torch
> python -c "import torch; print('torch OK:', torch.__version__)"

<br>
<br>

關鍵：用 --no-deps 先裝到底，再用正常模式解依賴，就能繞過 pip 解析器的「記憶效應」。<br>
現在照這做，保證一次成功！然後直接 python PPOCRLabel.py 啟動。<br>
<br>
<br>
<br>
<br>

## 這個版本 PPOCRLabel-v3.1.4:<br>
✔ 使用 Windows<br>
✔ 使用 Python 3.9.25<br>
✔ 使用 PaddlePaddle 3.2.2<br>
✔ 使用 PaddleOCR 3.3.2<br>
✔ 使用 Paddlex 3.3.10<br>
✔ 使用 Numpy 2.0.2<br>
✔ 使用 OpenCV 4.10.0.84<br>
<br>
<br>
<br>
<br>

### 使用 PPOCRLabel V3 來標籤識別物<br>
https://github.com/PFCCLab/PPOCRLabel

> conda create -n ocr python=3.9 -y<br>
> conda activate ocr
<br>

#### 1. 下載程式碼v3.1.4(非必要)
https://github.com/PFCCLab/PPOCRLabel/releases/tag/v3.1.4
<br>

#### 2. Install PaddlePaddle<br>
> pip install --upgrade pip<br>
pip的版本會更新到 25.3
<br>

#### CPU<br>
> pip install paddlepaddle -i https://www.paddlepaddle.org.cn/packages/stable/cpu/
<br>

#### 3. PPOCRLabel<br>
> pip install PPOCRLabel
<br>

#### 4. paddlex 的 OCR<br>
PPOCRLabel 3.1.4 使用了 PPStructureV3 表格檢測模組，因此 PaddleX 必須包含 OCR 功能。<br>
> pip install "paddlex[ocr]"
<br>

#### 5.執行 PPOCRLabel<br>
5-1.可直接用 PPOCRLabel<br>
(docs\5-1.直接呼叫.png)<br>
會等很久後才開啟，建議可以用程式碼的方式呼叫，就會知道他在下載相關模型，所以很久才會打開<br>
<br>

5-2.程式碼呼叫 python PPOCRLabel.py<br>
(docs\5-2.呼叫程式碼.png)
<br>

### ⭐ PPOCRLabel 標註的 4 大重點<br>
#### 1. 框要「剛好」包住字，不要太多空白<br>
框太大 → 模型會學到背景噪音<br>
框太小 → 字會被切掉<br>
<br>
理想：留一點點 padding，但不要太多，要能夠顯示完整車牌<br>
<br>
<br>

#### 2. 直線文字用水平框，多方向用四邊形框<br>
PPOCRLabel 支援：<br>
水平框（一般文字）<br>
四點框（旋轉文字）<br>
<br>
<br>

若字是歪的，要用四點框，不然模型會學錯形狀。<br>
幾何校正（仿射 / 透視）<br>
M = cv2.getPerspectiveTransform(points, pts_std)<br>
dst_img = cv2.warpPerspective<br>
(PPOCRLabel-3.1.4\lib\utils.py get_rotate_crop_image(img, points):)<br>
<br>
<br>

#### 3. 標註內容務必正確，模型完全依賴你輸入的文字<br>
你輸入的文字 = 模型的「答案」<br>
你若輸入錯字 → 模型會學壞<br>
<br>
所以「人工轉寫」非常重要。<br>
<br>
<br>

#### 4. 標註一致性要維持，否則模型會學亂<br>
例如：<br>
車牌 → 你要固定格式（比如不要有空白或額外符號）<br>
表格 → 要不要換行？要不要空格？都要統一<br>
發票 → 不要 A 框寫「123」，B 框寫「 123 」，格式要一樣<br>
<br>
模型是「機械學習」，它會根據你的資料風格學習。<br>
<br>
且要填寫正確車牌，像是髒污或是反光看不到字，不可忽略，要填寫真實答案<br>
例如:AB-2213，反光"-"看起來像是只有 AA 2213，但在填寫時，需寫出真實答案 AA-2213，不可少寫或是寫成其他數字(像是空白)<br>
<br>
<br>
<br>