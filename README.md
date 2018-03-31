# MobilityAid
Android Application using TensorFlow to detect common objects on the street.

Install Docker Toolbox
Open Docker QuickStart Terminal
to create new docker container: docker run -it gcr.io/tensorflow/tensorflow:latest-devel
CHECK CONTAINER NAME:   docker ps -a
to enter this container later: 	docker start CONTAINERNAME  
				                        docker attach CONTAINERNAME

//CONTAINERNAME = kind_fermat for this example

COPY FILES FROM WINDOWS TO DOCKER: (all files within the folder are copied, not the folder)
docker cp F:/#SJSU/AI/PROJECT/Training kind_fermat:/aiproject/Tests

COPY FILES FROM DOCKER TO WINDOWS: 
docker cp kind_fermat:/aiproject/Tests F:/#SJSU/AI/PROJECT/Testing

In docker, cd to / directory, then
#: cd tensorflow
#: git pull
cd ens
TRAINING:
IMAGE_SIZE=224
ARCHITECTURE="mobilenet_0.50_${IMAGE_SIZE}"

python tensorflow/tensorflow/examples/image_retraining/retrain.py \
--bottleneck_dir=/aiproject/bottlenecks \
--model_dir=/aiproject/inception \
--output_graph=/aiproject/retrained_graph.pb \
--output_labels=/aiproject/output_labels.txt \
--image_dir /aiproject/Train
--architecture="${ARCHITECTURE}" \
--summaries_dir=tf_files/training_summaries/"${ARCHITECTURE}" \

Testing:
python <script> <image_path> <label_file.txt> <graph_file.pb>
example: python /aiproject/label_test.py /aiproject/Testing/bench1.jpg /aiproject/output_labels.txt /aiproject/retrained_graph.pb
