node {
   def mvnHome
   stage('Preparation') {         
      mvnHome = tool 'Maven 2.2.1'
   }
   stage('Build') {
      // Run the maven build
      if (isUnix()) {
         sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore clean package"
      } else {
         bat(/"${mvnHome}\bin\mvn" -Dmaven.test.failure.ignore clean package/)
      }
   }
   stage('Results') {
      junit '**/target/surefire-reports/TEST-*.xml'
      archive 'target/*.jar'
   }
   stage('Publish') {
       nexusPublisher nexusInstanceId: 'Nexus', nexusRepositoryId: 'releases', packages: [[$class: 'MavenPackage', mavenAssetList: [[classifier: '', extension: '', filePath: 'target/maven-simple-0.2-SNAPSHOT.jar']], mavenCoordinate: [artifactId: 'maven-simple', groupId: 'om.github.jitpack', packaging: 'war', version: '0.2']]]
   }
}
