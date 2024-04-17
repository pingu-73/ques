---
layout: default
---

<style>
.center {
  display: block;
  margin-left: auto;
  margin-right: auto;
}
</style>

# Question 1:
At IIIT we use LDAP to manage user information — usernames, credentials, along with other metadata. Given that our LDAP url is [ldap.iiit.ac.in](http://ldap.iiit.ac.in/):

1. figure out how you can query the database for your own information
2. append a description field to your entry
3. show how you can use LDAP to find all the students in your batch

## Answer:
### Part1:
- First check the ip address for `ldap://ldap.iiit.ac.in/` using `nslookup` command.

<!-- ![nslookup.png](./assets/q1/nslook.png) -->
<img src="./assets/q1/nslook.png" alt="nslookup" class="center" width="300" height="200" >

- Now searching the baseObject to find out dn using `ldapsearch -H ldap://ldap.iiit.ac.in -x -b '' -s base'(objectclass=*)'`. From the output we can say that ldap is using standard naming conventions.
<!-- ![find_dns.png](./assets/q1/find_dn.png) -->
<img src="./assets/q1/find_dn.png" alt="find_dns.png" class = "center" width="300" height="200">

- Now from the above information to query database for my own information: i can use the following command: `ldapsearch -x -H ldap://ldap.iiit.ac.in -b "dc=iiit,dc=ac,dc=in" "(uid=dikshant.gurudutt)"`

<!-- ![ans-part1.png](./assets/q1/ans_part1.png) -->
<img src="./assets/q1/ans_part1.png" alt="ans-part1.png" class = "center" width="400" height="300">

### Part2:
- To append description field for `uid=dikshant.gurudutt` we can use `ldapmodify` command Altough appending description field should not be possible because in ldap enviroment client only has read access and not write/append access.
- But step would be to create a `LDIF` file containg `dn for pointing to my cn, changetype, add to specify name of attribute to be added, content.`

<!-- ![ans-part2.png](./assets/q1/part_2.png) -->
<img src="./assets/q1/part_2.png" alt="ans-part2.png" class = "center">

- As specified earlier I don't have write access to the ldap server.

### Part3:
Now from above steps we can say that to find out all the people in ug2k22. I need to change the filter and set correct base dn. So i’ve to set dn = `ou=ug2k22,ou=ug,ou=Students,ou=Users,dc=iiit,dc=ac,dc=in` and filter = `filter set = (objectClass=inetOrgPerson)` because `inetOrgPerson` represents user entries in ldap dirs.
Hence the command is used to just print common name and distinguished name for ug2k22 batch is : `ldapsearch -x -H ldap://ldap.iiit.ac.in -b "ou=ug2k22,ou=ug,ou=Students,ou=Users,dc=iiit,dc=ac,dc=in" "(objectClass=inetOrgPerson) cn"`

<!-- ![ans-part3.png](./assets/q1/part_3.png) -->
<img src="./assets/q1/part_3.png" alt="ans-part2.png" class = "center" width="50%" height="50%">

# Question 2:
You are an admin on a server with multiple users. You find an unknown process running. You don’t want to kill it yet. How do you determine what exactly the process is doing and whether it is malicious?
## Answer:

# Question3:
Suppose as a sysadmin, you need to figure out how to prevent students from connecting to machines outside IIIT over ssh (assume a regular configuration). For the purpose of this problem, assume that all traffic passes though a single Linux machine (think of it like your home Wi-Fi router) and it can run whatever you want it to (make reasonable assumptions).
1.  describe how you would accomplish this task using existing Linux tools and/or existing open source software.
2.  how does your answer change if you need to instead block http://facebook.com?
3.  (extra credit) how does your answer change if you need to instead block https://facebook.com?
4.  (extra credit) how does your answer change if you want to prevent clever students from trying to access ssh over non-standard ways?
## Answer

# Question4:
Suppose you want to run a website on your computer in the LAN. You want your friends to be able to access it with a URL like rishav.iiit.ac.in, but you do not want to get any official approval.
1.  Describe how you would go about it. What instructions you would give to your friends so they can access your website (bonus: will your solution work for any generic xyz.iiit.ac.in?)
2.  (extra credit) Suppose you wish to allow people anywhere on the internet to access your websites. What are the steps you think that us, as sysadmins, would have to follow?
## Answer:
