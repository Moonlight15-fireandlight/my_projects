# my_projects
resources:
- name: repo
  type: git
  source: 
    uri: https://github.com/Moonlight15-fireandlight/my_projects
jobs:
- name: hello-world-job
  plan:
  - get: repo
    trigger: true #le dice al concourse que active este file cuando se emitan nuevas versiones
  - task: hello-world-task
    config:
      platform: linux
      image_resource:
        type: registry-image
        source:
          repository: busybox
      inputs:
      - name: repo
      run:
        path: cat
        args: ["repo/README.md"]
