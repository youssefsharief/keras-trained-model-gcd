

* Create your model file locally
    * `python export_model_final.py`

* GCD
    * GCD Initial Setup
        * Create new project in GCD
        * Enable Billing
        * Make sure you are logged in `gcloud init`
    * Add the created model to GCD
        * Create a new google cloud bucket using `gsutil mb -l us-central1 gs://keras-class-1992`
        * Use the `gsutil cp` command to copy files from our computer to the cloud since we need to copy our model
            * `gsutil cp -R exported_model/* gs://keras-class-1992/earnings_v1`

    * GCD ml-engine
        * Create a new model in ml-engine service in GCD
            * `gcloud ml-engine models create earnings --regions us-central1`
        * Create a new version of the model and link that version to the model uploaded to the bucket
            * `gcloud ml-engine versions create v1 --model=earnings --origin=gs://keras-class-1992/earnings_v1 --runtime-version 1.2`
        * Predict
            * `gcloud ml-engine predict --model=earnings --json-instances=sample_input_prescaled.json`