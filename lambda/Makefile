MAKE_ARGS:=--profile $(AWS_PROFILE) --region $(AWS_REGION)

ACCOUNT_ID:=$(shell aws sts get-caller-identity $(MAKE_ARGS) --output text --query 'Account')

#  use existing cloudformation templates bucket to keep lambda function source codes
SAM_SOURCE_BUCKET:=cloudformation-$(AWS_REGION)-$(ACCOUNT_ID)

build:
	GOOS=linux GOARCH=amd64 go build -o src/main src/main.go
create-bucket:
	aws s3 mb s3://$(SAM_SOURCE_BUCKET) $(MAKE_ARGS)
run:
	sam local start-lambda
package:
	sam package --template-file build/saml.yaml --output-template-file build/packaged.yaml --s3-bucket $(SAM_SOURCE_BUCKET) $(MAKE_ARGS)
deploy:
	sam deploy --template-file build/packaged.yaml --stack-name hello_lambda \
		--capabilities CAPABILITY_IAM $(MAKE_ARGS) \
		--parameter-overrides EnvironmentName=$(ENV_LABEL)
