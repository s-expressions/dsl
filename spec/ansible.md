# S-expression standard: Ansible

## Status

Draft

## Abstract

This document defines an S-expression representation of Ansible
playbooks.

## Rationale

Ansible is a popular tool for remotely configuring operating systems
and application software on servers and other computers. It uses a
configuration language that is mostly declarative. However, parts of
the language are imperative for the sake of practicality.

The native format for an Ansible configuration is a directory tree
with many subdirectories, most of them containing little YAML files.
Some strings in the YAML files are expanded as Jinja templates.

A sprawling directory tree with many small files is unwieldy for to
maintain and the nested syntaxes of YAML and Jinja, each with its own
irregularities, is difficult to keep under one's intellectual control.

We believe that Ansible's robust module set is much better designed
than its ad hoc configuration syntax, and that the syntax problem is
effectively solved by a simple and consistent S-expression wrapper.

## Specification

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
