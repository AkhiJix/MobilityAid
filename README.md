# MobilityAid
- Android Application using TensorFlow to detect common objects on the street.  
- This project was developed as a part of the coursework _CS256-Topics in Artificial Intelligence_ under the supervision of Dr. Natalia Khuri at San Jose State University during Aug-Dec 2017.  
- The team members include [Shantanu Deshmukh](https://github.com/shantanuspark) and [Saketh Saxena](https://github.com/sakethsaxena).  

## Instructions:  
- Install Docker Toolbox  
- Open Docker QuickStart Terminal  
- To create a new docker container: `docker run -it gcr.io/tensorflow/tensorflow:latest-devel`  
- CHECK CONTAINER NAME: `docker ps -a`  
- To enter this container:   
`docker start CONTAINERNAME`  
`docker attach CONTAINERNAME`  

> CONTAINERNAME = kind_fermat for this example

- COPY FILES FROM WINDOWS TO DOCKER: (all files within the folder are copied, not the folder)  
`docker cp F:/#SJSU/AI/PROJECT/Training kind_fermat:/aiproject/Tests`  

- COPY FILES FROM DOCKER TO WINDOWS:  
`docker cp kind_fermat:/aiproject/Tests F:/#SJSU/AI/PROJECT/Testing`  

- Insde the container, execute the following commands:  
`#: cd tensorflow`  
`#: git pull`  

## Training:   
`IMAGE_SIZE=224`  
`ARCHITECTURE="mobilenet_0.50_${IMAGE_SIZE}"`  

`python tensorflow/tensorflow/examples/image_retraining/retrain.py \`  
`--bottleneck_dir=/aiproject/bottlenecks \`  
`--model_dir=/aiproject/inception \`  
`--output_graph=/aiproject/retrained_graph.pb \`  
`--output_labels=/aiproject/output_labels.txt \`  
`--image_dir /aiproject/Train \`  
`--architecture="${ARCHITECTURE}" \`  
`--summaries_dir=tf_files/training_summaries/"${ARCHITECTURE}"`  

## Testing:  
`python <script> <image_path> <label_file.txt> <graph_file.pb>`  
- Example:   
`python /aiproject/label_test.py`   
`/aiproject/Testing/bench1.jpg`   
`/aiproject/output_labels.txt`   
`/aiproject/retrained_graph.pb`  

## Android  
Once the model is trained, the retrained_graph.pb file and the labels.txt files should be linked to the android application. The detailed steps and the pertaining files can be found on [Shantanu's Github](https://github.com/shantanuspark/tensorflowMobilityAid), who was responsible for the android application developement.  

## Download the Android App and related files   
The trained model, training labels, training images, testing images, and the apk file can be accessed [here](https://drive.google.com/drive/folders/0B-rL_pZzer0zUUNyaVlfOUI4TlE?usp=sharing). 
