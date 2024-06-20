# FitMotion - Motion Sensing App for Improving and Optimizing Physical Fitness
FitMotion is a Fitness Apps that detects users activities to determines their activity levels and helps users reach their fitness goals

## Machine Learning
FitMotion model starts off from a dataset we gathered from kaggle (https://www.kaggle.com/datasets/malekzadeh/motionsense-dataset/code).

This dataset is collected with an iPhone 6 gyro sensor, this means that the data from our android needs to be fitted to be properly detected by the model trained from the dataset.

### Data Cleaning and Model Training
123
### Android Data Gathering and Fitting
123
### Testing ML Model
123

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
