# FitMotion - Motion Sensing App for Improving and Optimizing Physical Fitness
FitMotion is a Fitness Apps that detects users activities to determines their activity levels and helps users reach their fitness goals

# Machine Learning (fitmotion-model)
FitMotion model starts off from a dataset we gathered from kaggle (https://www.kaggle.com/datasets/malekzadeh/motionsense-dataset/code).

This dataset is collected with an iPhone 6 gyro sensor, this means that the data from our android needs to be fitted to be properly detected by the model trained from the dataset.

## Data Training
With model_training.ipynb we can define the dataset used to train the model, fitmotion initally uses all data from the dataset, but decided only to use the Gravity and Acceleration data (reduced).

```python
# change these following three lines only
reduced = True
operating_system = 'linux' #windows or linux
subject_data_file = 'data_subjects_info.csv'
```

the model is then saved into the the models folder to be inferenced.

## Data Testing
To test data collected we cab yse the model_tester.ipynb file, by first choosing which model you want to use.

```python
# Specify Model
reduced = False
model_type = 'keras' # keras or h5 or onnx
factor_index = 0
```

we then load the data to predict the movement

```python
# Load Android Data
data_source = 'android_data_latest'
if reduced:
    data_source += '_reduced'
data_type = 'wlk'
data_num = '5'
data_url = '../data/' + data_source + '/' + data_type + '/' + data_type + data_num + '-SensorData.csv'

df = pd.read_csv(data_url, sep=',')
    
df = df.drop(['Unnamed: 0'], axis=1) if 'Unnamed: 0' in df.columns else df
df = df.drop(['id'], axis=1) if 'id' in df.columns else df
df
```

after some preprocessing, the data is then passed to the train model to predic the movement which outputs as such
```
wlk
```

# Cloud Computing

## FitMotion-Core 
Built with [FastAPI](https://fastapi.tiangolo.com/). FitMotion-Core is main Backend of FitMotion App.
<hr />

### Initial Configuration
1. Create an environment. It is recommended using pipenv or virtualenv
```bash
# using virtualenv
vitualenv .venv

# For Linux
source .venv/bin/activate
# For Windows
.venv\Scripts\activate

# using  pipenv
pipenv shell
```
3. Install the dependencies
```bash
# using pipenv
pipenv install

# using pip
pip install -r requirements.txt
```
5. Create new `.env.development` file and add following variables: `PG_URL`, `SECRET`, `ALGORITHM`, `GOOGLE_APPLICATION_CREDENTIALS`, `CLOUD_BUCKET`. Your `.env.development` file should look like this.
```
# .env.development
PG_URL= <database connection string>
SECRET= <secret hex>
ALGORITHM=HS256
GOOGLE_APPLICATION_CREDENTIALS= <location of google cloud storage service account json key>
CLOUD_BUCKET= <bucket name>
```
6. Run the server. You can run the server using the pre-configured `Makefile` with command `make dev`. You can also start the server with uvicorn command.
```
# hot reload for development
uvicorn src.main:app --reload

# exposed to public for production
uvicorn src.main:app --host 0.0.0.0 --port 0.0.0.0
```
## Fitmotion Prediction Service

### Quick setup
1. Create new `.env` file and add Cloud Storage JSON service account key location as `GOOGLE_APPLICATION_CREDENTIALS` variable

2. Install the dependencies
```bash
pip install -r requirements.txt
pip install onnxruntime

# You can also use pipenv instead
pipenv shell
pipenv install
```

3. Start the server
```bash
uvicorn main:app --host 0.0.0.0 --port 8080
```


# Mobile Development
