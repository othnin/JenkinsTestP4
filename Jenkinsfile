pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                sh ''' 
                    #!/bin/bash
                    echo $PWD
                    PATH=$WORKSPACE/venv/bin:/usr/bin:$PATH
                    PYENV_HOME=$WORKSPACE/.pyenv/
                    # Delete previously built virtualenv
                    if [ -d $PYENV_HOME ]; then
                      rm -rf $PYENV_HOME
                    fi

                    # Create virtualenv and install necessary packages
                    virtualenv --no-site-packages $PYENV_HOME
                    . $PYENV_HOME/bin/activate
                    pip install -r requirements.txt
                    pip install --quiet nosexcover
                    pip install --quiet pylint
                    pip install --quiet $WORKSPACE/  # where your setup.py lives
                    nosetests --with-xcoverage --with-xunit --cover-erase
                    pylint -f parseable JenkinsTestP4/ | tee pylint.out
                    #. venv/bin/activate
                    #pip install -r requirements.txt
                    #python test.py
                '''
            }
        }
    }
}



