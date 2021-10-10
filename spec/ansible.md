# S-expression standard: Ansible

## Status

Draft

## Abstract

This document defines an S-expression representation of Ansible
playbooks.

## Rationale

```Lisp
(define-schema ansible

  (ansible
    `(ansible
       (options ,@var)
       (groups ,@group)
       (playbooks ,@playbook)
       (roles ,@role)))

  (var
    `(var ,symbol ,any))

  (group
    `(group
       (name ,symbol)
       (hosts ,@host)))

  (host
    `(host
       (name ,symbol)
       (vars ,@var)))

  (playbook
    `(playbook
       (name ,symbol)
       (hosts ,@symbol)
       (become ,boolean)
       (roles ,@symbol)))

  (role
    `(role
       (name ,string)
       (tasks ,@task)
       (handlers ,@handler)
       (files ,@file)))

  (task
    `(task
       (name ,string)
       ,module))

  (handler
    `(handler
       (name ,string)
       ,module))

  (module
    `(,symbol
      ,@parameter))

  (parameter
    `(,symbol ,any))

  (file
    `(file
       (name ,string)
       (content ,string))))
```

## Examples

```Lisp
(ansible

 (options)

 (groups
  (group
   (name example-hosts)
   (hosts
    (host
     (name localhost)
     (vars
      (var ansible-host "localhost"))))))

 (playbooks
  (playbook
   (name hello)
   (hosts example-hosts)
   (become true)
   (roles
    write-hello-world)))

 (roles

  (role
   (name write-hello-world)
   (tasks
    (task
     (title "write a hello file to /tmp")
     (copy
      (dest "/tmp/hello")
      (content "Hello world")))))))
```

## Rerefences
