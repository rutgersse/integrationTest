An integration test is:
1-A test uses the database
2-A test uses the network
3-A test uses an external system (e.g. a queue or a mail server)
4-A test reads/writes files or performs other I/O

a-For an integration test,results also depends on external systems in addition to the code.
b-Setup of integration test might be complicated
c-One or more components are tested
d-No mocking is used (or only unrelated components are mocked)
e-Test verifies implementation of individual components and their interconnection behaviour when they are used together
f-An integration test can use real containers and real DBs as well as special integration testings frameworks (e.g. Arquillian or DbUnit)
g-Integration tests are also useful to QA, DevOps, Help Desk
h-A failed integration test can also mean that the code is still correct but the environment has changed
i-ntegration tests in an Enterprise application can last for hours

The suggested workflow for running the integration test would be:
1-Developers run the test goal during development
2-Developers run the test goal before any commit
3-Developers run the integration-test goal before a major commit with many side effects
4-Build server compiles code and runs the test goal every 15-30 minutes (main build)
5-Build server compiles code and runs the integration-test goal every day (integration build)
6-Build server compiles code and runs the integration-test goal before a release to QA

We use Jenkins for integration and contionuois integration.
Continuous Integration (CI) is a development practice that requires developers to integrate code into a shared repository several times a day. 
Each check-in is then verified by an automated build, allowing teams to detect problems early.

Installinh Jenkins

### Add the Jenkins repository to the list of repositories
$ sudo sh -c 'echo deb http://pkg.jenkins-ci.org/debian binary/ > /etc/apt/sources.list.d/jenkins.list'

### Add the repository's public key to your system's trusted keychain
$ wget -q -O - http://pkg.jenkins-ci.org/debian/jenkins-ci.org.key | sudo apt-key add -

### Download the repository index and install
$ sudo apt-get update
$ sudo apt-get install jenkins

$ sudo chown jenkins /webapps/hello_django/trunk/
jenkins ALL=NOPASSWD: /usr/sbin/apachectl
curl http://test-server:8080/job/hello-django-trunk/build?token=xZrJ5WsSfJkGpNsriOlY4PtQ7hC5olzDhNE

curl http://test-server:8080/buildByToken/build?job=hello-django-trunk&token=xZrJ5WsSfJkGpNsriOlY4PtQ7hC5olzDhNE
Build:
source /webapps/hello_django/activate     # Activate the virtualenv
cd /webapps/hello_django/trunk/
pip install -r REQUIREMENTS.txt           # Install or upgrade dependencies
python manage.py migrate                  # Apply South's database migrations
python manage.py compilemessages          # Create translation files
python manage.py collectstatic --noinput  # Collect static files
sudo apachectl graceful                   # Restart the server, e.g. Apache
python manage.py test --noinput app1 app2 # Run the tests

We did followig integration test:
csslint- Perform css compilation and systax check
jshint- Perform jshint compilation and systax check
pep8- Perform standard python syntax test
pylint- Perform lint test for python and compilation
main integration- Perform compilation and inter dependent sub modules and verification
dbIntegration- Perform database integration checks
Jenkins- Perform all above integration test automatically and continuosly update on our main server

Furthermore we are using travis build for integration test of individual componenent
i.e. main bcakend and twitter backend 
