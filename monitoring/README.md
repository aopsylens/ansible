# Requirements
```
ansible-galaxy install -r requirements.yaml
```

# Alertmanager error
if your alertmanager template doesn't render, then edit one task "copy alertmanager config"  in file" .ansible/roles/cloudalchemy.alertmanager/tasks/configure.yml

```
- name: copy alertmanager config
  template:
    force: true
    src: "{{ alertmanager_config_file }}"
    dest: "{{ alertmanager_config_dir }}/alertmanager.yml"
    owner: alertmanager
    group: alertmanager
    mode: 0644
    validate: "/usr/local/bin/amtool --alertmanager.url=  check-config %s"
  notify:
    - restart alertmanager
```

and change "copy file" instead "copy template
```
- name: copy alertmanager config
  copy:
    src: "{{ alertmanager_config_file }}"
    dest: "{{ alertmanager_config_dir }}/alertmanager.yml"
    owner: alertmanager
    group: alertmanager
    mode: 0644
  notify:
    - restart alertmanager
```
