we have to delete the app directory to avoid conflicts after that we can create again for that we have module in ansible
- name: Recursively remove directory
  ansible.builtin.file:
    path: /app
    state: absent
