# convert-tflite-for-android-
## Step 1 : run python export_tflite_ssd_graph.py 
python export_tflite_ssd_graph.py --pipeline_config_path=/home/cavid/Desktop/YouTube_object_detection/models/research/object_detection/training/ssd_mobilenet_v2_quantized_300x300_coco.config --trained_checkpoint_prefix=training/model.ckpt-70573  --output_directory=./tflite --add_postprocessing_op=true

## Step 2 : clone the git anywhere in your computer:
git clone git@github.com:tensorflow/tensorflow.git 


## step 3 : Run this code into tensorflow: /home/cavid/tensorflow ( here is my path) :
### - change the input_file and output_file localion

bazel  run -c opt  tensorflow/lite/toco:toco -- \
--input_file=/home/cavid/Desktop/YouTube_object_detection/models/research/object_detection/tflite/tflite_graph.pb \
--output_file=/home/cavid/Desktop/YouTube_object_detection/models/research/object_detection/tflite/result/detect.tflite \
--input_shapes=1,300,300,3 \
--input_arrays=normalized_input_image_tensor \
--output_arrays='TFLite_Detection_PostProcess','TFLite_Detection_PostProcess:1','TFLite_Detection_PostProcess:2','TFLite_Detection_PostProcess:3' \
--inference_type=QUANTIZED_UINT8 \
--mean_values=128 \
--std_values=128 \
--change_concat_input_ranges=false \
--allow_custom_ops


