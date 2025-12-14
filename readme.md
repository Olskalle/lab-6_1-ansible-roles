Структура  файлов, которая получится в итоге:

![Pasted image 20251214170022.png](attachments/Pasted%20image%2020251214170022.png)

Создаем конфиг для роли, создаем задачи на установку nginx и копирование конфига для виртуального хоста:

![Pasted image 20251214170305.png](attachments/Pasted%20image%2020251214170305.png)

Создаем шаблоны стартовой страницы и конфига:

![Pasted image 20251214170457.png](attachments/Pasted%20image%2020251214170457.png)

![Pasted image 20251214170518.png](attachments/Pasted%20image%2020251214170518.png)

Копирование стартовых страниц:

``` yaml
- name: Create site folders
  file:
    path: '/var/www/{{ item }}'
    state: directory
  loop: '{{ sites }}'

- name: Copy index from templates
  template:
    src: 'index.html.j2'
    dest: '/var/www/{{ item }}/index.html'
    owner: root
    group: root
    mode: '0644'
  loop: '{{ sites }}'
```

Создаем плейбук и запускаем и проверяем:

![Pasted image 20251214170910.png](attachments/Pasted%20image%2020251214170910.png)
