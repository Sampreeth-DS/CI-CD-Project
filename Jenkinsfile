properties([
    parameters([
	choice(name: 'ENV', choices: ['dev', 'test', 'prod', 'deploy'], description: 'Select the deployment environment'),
	string(name: 'NAME', defaultValue: 'apple,mango,orange', description: 'Enter the fruit name in comma separated format')
    ])
])

pipeline {
    agent any
    stages {
        stage('Dev') {
	        when{
		        expression { params.ENV=='dev' }
	        }
	        parallel{
	            stage('dev1'){
                    steps {
                        script{
        		            def fruits = params.NAME.split(',')
                            echo "Hello, This is a dev environment"
        		            for (fruit in fruits){
        			            echo "Fruit: $fruit"
        		            }
        		        }
                    }
	            }
	            stage('dev2'){
                    steps {
                        script{
        		            def fruits = params.NAME.split(',')
                            echo "Hello, This is a dev environment"
        		            for (fruit in fruits){
        			            echo "Fruit: $fruit"
        		            }
        		        }
                    }
	            }
	        }
        }
	    stage('Test') {
	        when{
		        expression { params.ENV=='test' }
	        }
            steps {
                script{
		            def fruits = params.NAME.split(',')
                    echo "Hello, This is a test environment"
		            for (fruit in fruits){
			            if (fruit == "apple") {
                            echo "$fruit detected -> Apple is processing"
                        } 
			            else if (fruit == "mango") {
                            echo "$fruit detected -> Mango is processing"
                        }
			            else {
			                echo "Processing other fruit: $fruit"
			            }

		            }
		        }
            }
        }
	    stage('Prod') {
	        when{
		        expression { params.ENV=='prod' }
	        }
            steps {
                script{
                    echo "Hello, This is a prod environment"
                }
                sh '''
                    echo "Listing block devices:"
                    lsblk
                    echo "Creating a directory sample"
                    mkdir /tmp/sample
                    echo "Displaying the directory"
                    ls /tmp
                    echo "Getting inside the directory"
                    cd /tmp/sample
                    echo "creating a sample file"
                    touch sample.sh
                    echo "Listing file with details"
                    ls -la
                    echo "Changing file permissions to execute"
                    chmod +x sample.sh
                    echo "Listing file with details"
                    ls -la
                '''
            }
        }
        stage('Deploy') {
	        when{
		        expression { params.ENV=='deploy' }
	        }
            steps {
                sh '''
                    echo "Hello, This is a deploy environment"
                    for fruit in $(echo "$NAME" | tr ',' ' '); do
                        if [ "$fruit" = "apple" ]; then
                            echo "$fruit detected -> Apple is processing"
                        elif [ "$fruit" = "mango" ]; then
                            echo "$fruit detected -> Mango is processing"
                        else
                            echo "Processing other fruit: $fruit"
                        fi
                    done
                '''
            }
        }
    }
    
    post {
        always {
            echo "This is a post stage execution!!!"
        }
    }
}
