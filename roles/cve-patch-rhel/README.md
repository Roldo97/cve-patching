Role Name
=========

This role will aid you in the installation of one or more specific CVE on your RHEL servers.

After the given CVEs are installed, it will send an email with an attached CVS file, called "report.csv", with a summary of the hosts involved in the play, the CVE installed on each, and if the host need to be rebooted or not after installing the CVE.

NOTE: when several CVEs are installed on the host, if one of those CVE requires a reboot, the "REBOOT REQUIRED" column in the report will be marked as true for all host rows, despite if the CVE requires or not a reboot.

This role has been tested with:
  - RHEL 7
  - RHEL 8
  - RHEL 9

Requirements
------------

This role depends on the "community.general" collection, used to send a report of the installed CVEs through mail.

Role Variables
--------------

| Variable       | Description                                                                      | Sample value                                                                        |
| -------------- | -------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- |
| host_to_apply  | The hosts or groups where you need to install the CVEs                           |                                                                                     |
| cves           | The CVE that you need to install. Can be one or more (separated by spaces).      | *   CVE-2024-24806
    
*   CVE-2024-24806 CVE-2023-31346 CVE-2024-4032             |
| reboot         | Reboots the hosts if one of the installed CVE requires a reboot to be effective. | *   true
    
*   false                                                             |
| mail_smtp_host | The address of the host used to send the report through mail.                    | *   smtp.freesmtpservers.com
    
*   172.16.X.X |
| mail_subject   | The subject of the email being sent.                                             |                                                                                     |
| mail_body      | The body of the email being sent.                                                |                                                                                     |
| mail_sender    | The email-address the mail is sent from. May contain address and phrase.         |                                                                                     |
| mail_recipient | The email-address(es) the mail is being sent to.                                 |                                                                                     |

Dependencies
------------

This role doesn't have dependencies on others.

Example Playbook
----------------

Including an example of how to use your role (dfor instance, with variables passed in as parameters) is always nice for users too:

When running from CLI:
```
ansible-playbook patch-cve.yml -e "cves='CVE-2024-5564 CVE-2024-24806'" -e "reboot=false" -e "host_to_apply=all" -e "mail_smtp_host=smtp.example.com" -e "mail_subject='CVE Patching'" -e "mail_body='Please, find the installed CVE report in the attachments.'" -e "mail_sender=sender@example.com" -e "mail_recipient=recipient@example.com"
```
This will install the CVEs "CVE-2024-5564" and "CVE-2024-24806" on all hosts, and will reboot the hosts if one of the installed CVE requires it to be effective.

The content of the "patch-cve.yml" playbook:
```
    - hosts: "{{ host_to_apply | default('localhost') }}"
      roles:
         - cve-patch-rhel
```

License
-------

BSD

Author Information
------------------

[github.com/Roldo97](https://github.com/Roldo97)
