pipeline {
   
    agent any
       stages {
           stage ('Complie Stage') {
             
            steps{
            withMaven(maven : 'Maven_home'){
             sh 'mvn clean compile'
}
           
}
}

       stage ('Testing Stage'){
       steps {
               withMaven(maven : 'Maven_home'){

               sh 'mvn test'
}
}
}

}
}
