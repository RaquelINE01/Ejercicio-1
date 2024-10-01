pipeline {
    agent any
 
    environment {
        WEATHER_API_KEY = credentials('weather-api-key') // Store your API key in Jenkins credentials
    }
 
    stages {
        stage('Fetch Weather Forecast') {
            steps {
                script {
                    def city = 'London'
                    def response = sh(script: "curl -s 'http://api.openweathermap.org/data/2.5/weather?q=${city}&appid=${WEATHER_API_KEY}'", returnStdout: true).trim()
                    def weather = readJSON text: response
                    def forecast = weather.weather[0].description
                    writeFile file: 'forecast.txt', text: "Current weather in ${city}: ${forecast}\n"
                }
            }
        }
    }
 
    post {
        always {
            archiveArtifacts artifacts: 'forecast.txt', allowEmptyArchive: true
        }
    }
}
