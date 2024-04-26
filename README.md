# ansible-playbook
A GitHub Workflow action to run Ansible playbooks.

# Usage

```yaml
jobs:
  test:
    runs-on: ubuntu-latest
    steps:

      - name: "Apply playbook"
        uses: alex-oleshkevich/ansible-playbook@VERSION
        with:
            inventory-file: "assets/inventory.ini"
            playbook-file: "assets/playbook.yml"
            private-key: |
                -----BEGIN OPENSSH PRIVATE KEY-----
                              ...
                -----END OPENSSH PRIVATE KEY-----
            become-password: "password"
            become-user: "root"
            become-method: "sudo"
            tags: >-
              tag1
              tag2
            skip-tags: >-
              tag3
              tag4
            vault-password: "vault_password"
            check-only: "true"
            user: "user"
            debug: "true"
            extra_variables: >-
              key1=value1
              key2=value2
            options: "--verbose -T 20"

      - name: "Print Ansible version"
        run: ansible-playbook --version
```

Note on multiline strings. We don't support new line characters. Using new line characters, for example, in `extra_variables` will cause error.
```yaml
# don't

extra_variables: |
  key1=value1
  key2=value2

# do
extra_variables: >-
  key1=value1
  key2=value2

extra_variables: key1=value1 key2=value2
```
