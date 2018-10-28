## 生成coco TFRecord文件
* 在models/research/路径下创建coco文件夹
```
mkdir coco
cd coco
ln -s ~/data/coco/images/ ./
ln -s ~/data/coco/annotations/ ./
```

* 生成TFRecord文件
```
在models/research路径下
python object_detection/dataset_tools/create_coco_tf_record.py 
--train_image_dir=~/data/coco/train2017/ 
--val_image_dir=~/data/coco/val2017 
--test_image_dir=~/data/coco/test2017 
--train_annotations_file=~/data/coco/annotations/instances_train2017.json 
--val_annotations_file=~/data/coco/annotations/instances_val2017.json 
--testdev_annotations_file=~/data/coco/annotations/image_info_test-dev2017.json 
--output_dir=./
```

```
文件结构如下：
+ object_detection
	+ data 
		+ coco_train.record-*
		+ coco_val.record-*
		+ coco_testdev.record-*
```

* 在Tensorflow detection model zoo中下载模型， 比如ssd_resnet_50_fpn_coco。把下载的模型解压后放在object_detection/models路径下面。文件结构如下：

```
+ object_detection
	+ models
		+ ssd_resnet50_v1_fpn
			+ saved_model
			- checkpoint
			- frozen_inference_graph.pb
			- model.ckpt.data-00000-of-00001
			- model.ckpt.index
			- model.ckpt.meta
			- pipeline.config
```

* 修改pipeline.config中的“PATH_TO_BE_CONFIGURED”，替换为指定的路径。
* 开始训练：
```
python object_detection/model_main.py 
--model_dir object_detection/ssd_resnet50_v1_fpn/saved_model
--pipeline_config_path object_detection/ssd_resnet50_v1_fpn/pipeline.config
--num_trian_steps 250000
--alsologtostderr
```






















