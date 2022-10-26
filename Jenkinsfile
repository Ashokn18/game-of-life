pipeline{
		agent {
			node {
				label "build-in"
				customWorkspace "/mnt/project"
			}
		}	
			stages {
				stage ('build project'){
					steps {
					/*sh "rm -rf /root/.m2"*/
					sleep 5
					sh "mvn clean install"
					
					}
				}
				
				stage ('diploy war') {
					steps {
						sh "cp -r /mnt/git-project/gameoflife-web/target/gameoflife.war /mnt/docker"
						
						}
					}
					
				stage ('create custom image by docker file') {
					steps {
						dir ('/mnt/docker'){
						sh "chmod -R 777 gameoflife.war"
						sh "docker build -t mytomcat ."
						}
						}
					}	
				stage ('create container') {
					steps {
						
						sh "docker run --name my-container -itdp 8888:8080 mytomcat"
						
						}
					}	
				
				}
				
	}
