Ansible depend handler test
===========================

To run the test:

.. code-block:: console

   user@host:~$ ./play.yml

Example wrong output on Ansible devel (af249b83):

.. code-block:: console

   PLAY [localhost] ***************************************************************

   TASK [setup] *******************************************************************
   ok: [localhost]

   TASK [dependency-one : Notify Dependent Handler 1] *****************************
   changed: [localhost]

   TASK [dependency-two : Notify Dependent Handler 2] *****************************
   changed: [localhost]

   TASK [role-with-dependencies : Notify Handler 1] *******************************
   changed: [localhost]

   RUNNING HANDLER [role-with-dependencies : Handler 1] ***************************
   changed: [localhost]

   PLAY [localhost] ***************************************************************

   TASK [setup] *******************************************************************
   ok: [localhost]

   TASK [dependency-one : Notify Dependent Handler 1] *****************************
   changed: [localhost]

   TASK [dependency-two : Notify Dependent Handler 2] *****************************
   changed: [localhost]

   TASK [role-no-dependencies : Notify Handler 2] *********************************
   changed: [localhost]

   RUNNING HANDLER [dependency-one : Dependent Handler 1] *************************
   changed: [localhost]

   RUNNING HANDLER [dependency-two : Dependent Handler 2] *************************
   changed: [localhost]

   RUNNING HANDLER [role-no-dependencies : Handler 2] *****************************
   changed: [localhost]

   PLAY RECAP *********************************************************************
   localhost                  : ok=12   changed=10   unreachable=0    failed=0

Example right-ish output on Ansible stable-2.1 (dd15a15e):

.. code-block:: console

   PLAY [localhost] ***************************************************************

   TASK [setup] *******************************************************************
   ok: [localhost]

   TASK [dependency-one : Notify Dependent Handler 1] *****************************
   changed: [localhost]

   TASK [dependency-two : Notify Dependent Handler 2] *****************************
   changed: [localhost]

   TASK [role-with-dependencies : Notify Handler 1] *******************************
   changed: [localhost]

   RUNNING HANDLER [role-with-dependencies : Handler 1] ***************************
   changed: [localhost]

   RUNNING HANDLER [dependency-one : Dependent Handler 1] *************************
   changed: [localhost]

   RUNNING HANDLER [dependency-two : Dependent Handler 2] *************************
   changed: [localhost]

   PLAY [localhost] ***************************************************************

   TASK [setup] *******************************************************************
   ok: [localhost]

   TASK [dependency-one : Notify Dependent Handler 1] *****************************
   changed: [localhost]

   TASK [dependency-two : Notify Dependent Handler 2] *****************************
   changed: [localhost]

   TASK [role-no-dependencies : Notify Handler 2] *********************************
   changed: [localhost]

   RUNNING HANDLER [dependency-one : Dependent Handler 1] *************************
   changed: [localhost]

   RUNNING HANDLER [dependency-two : Dependent Handler 2] *************************
   changed: [localhost]

   RUNNING HANDLER [role-no-dependencies : Handler 2] *****************************
   changed: [localhost]

   PLAY RECAP *********************************************************************
   localhost                  : ok=14   changed=12   unreachable=0    failed=0

Example right output on Ansible stable-2.0 (de3f0131):

.. code-block:: console

   PLAY [localhost] ***************************************************************

   TASK [setup] *******************************************************************
   ok: [localhost]

   TASK [dependency-one : Notify Dependent Handler 1] *****************************
   changed: [localhost]

   TASK [dependency-two : Notify Dependent Handler 2] *****************************
   changed: [localhost]

   TASK [role-with-dependencies : Notify Handler 1] *******************************
   changed: [localhost]

   RUNNING HANDLER [dependency-one : Dependent Handler 1] *************************
   changed: [localhost]

   RUNNING HANDLER [dependency-two : Dependent Handler 2] *************************
   changed: [localhost]

   RUNNING HANDLER [role-with-dependencies : Handler 1] ***************************
   changed: [localhost]

   PLAY [localhost] ***************************************************************

   TASK [setup] *******************************************************************
   ok: [localhost]

   TASK [dependency-one : Notify Dependent Handler 1] *****************************
   changed: [localhost]

   TASK [dependency-two : Notify Dependent Handler 2] *****************************
   changed: [localhost]

   TASK [role-no-dependencies : Notify Handler 2] *********************************
   changed: [localhost]

   RUNNING HANDLER [dependency-one : Dependent Handler 1] *************************
   changed: [localhost]

   RUNNING HANDLER [dependency-two : Dependent Handler 2] *************************
   changed: [localhost]

   RUNNING HANDLER [role-no-dependencies : Handler 2] *****************************
   changed: [localhost]

   PLAY RECAP *********************************************************************
   localhost                  : ok=14   changed=12   unreachable=0    failed=0

