### Github Documentation
https://github.com/marketplace/actions/aws-lambda-deploy

### Template
```
name: Deploy lambda function
on: 
  push:
    branches:
      - main
jobs:
  build-lambda:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v3
    - name: Generate output.zip
      run: |
        npm install
        zip -r output.zip *
    - name: Upload output.zip to S3
      uses: jakejarvis/s3-sync-action@master
      env:
        AWS_S3_BUCKET: ${{ secrets.AWS_S3_BUCKET }}
        AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
        AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
        AWS_REGION: 'eu-central-1'   
        SOURCE_DIR:  output.zip    
```