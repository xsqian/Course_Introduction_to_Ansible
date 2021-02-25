### to run the upload task only:
    ansible-playbook playbooks/setup-app.yml --tags upload

### to run all the tasks except the upload
    ansible-playbook playbooks/setup-app.yml --skip-tags upload