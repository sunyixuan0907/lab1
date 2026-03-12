3.10：20.03
# commom/config
该文件定义常量
- BLOCK_SIZE 这个参数做了实验，[实验文件](../../../test/argument_test.py)

# common/pattern
该文件定义一些常见样式
- 用numpy创建多维数组带更多可用的对象方法

# encoder/frame_builder
这是帧生成
## draw_pattern
一个函数实现对finder块和align块的作画
- 调用相应的pattern生成函数和大小（5/7）
## build_template
该函数作画模板帧，结合draw_pattern 讲讲一些参数的计算
- 按8逻辑像素为1块的话，总共有135行（0-based）
- 第0块的逻辑像素开始于0逻辑像素，结束于第4逻辑像素，所以第n块<br>
开始于第 n * BLOCK_SIZE,结束于 n * (BLOCK_SIZE + 1) - 1,用0based去数第几块就不会混乱
- 举ALIGN块，ALIGIN块应该开始于第130行，结束于第134行，所以用GRID_ROWS - ALIGN_SIZE
# decoder
## decoder/frame_reader.py 
- 使用 cv2.VideoCapture 读取视频
- read_frames(video_path) 以生成器方式逐帧 yield 原始 BGR 帧（不做灰度化或其它图像处理）
- 帧类型保持 OpenCV 默认：np.ndarray，shape=(H, W, 3)，dtype=uint8
- 文件不存在时抛出 FileNotFoundError
- 文件存在但无法打开时抛出 RuntimeError
- get_video_info(video_path) 返回 frame_count / fps / width / height
