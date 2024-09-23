
# Host Intrusion Detection

---
## About
* Monitor **systems** for signs of suspicious activity
* Look for behaviours associated with
	* Humans or applications
	* Behaving suspiciously
	* Attempting to carry out an attack
	* / already compromised host

### HIDS vs NIDS
Network based intrusion detection system (NIDS) looks for suspicious activity on the network FROM PERSPECTIVE OF NETWORK (e.g. logs on switches, etc)

HIDS looks at things from perspective of HOST (can reveal backdoors that NIDS can't? (i guess would normally need network to exploit))

---
## Capabilities

* HIDS should **alert** response team intelligently when there is an action that needs taking (and not more frequently: alert fatigue)
* Generate reports
	* Big picture (overall state of system): stats about detection frequency/category etc over time
* Response
	* e.g. DoS attack detected: generate firewall rule to block src IP

### Limitations
Only one layer of security stack
Cannot detect compromised src code etc

---
## Building a HIDS

### Agent-based vs Agentless

#### Agent-based HIDS
* **software installed on host**
* uses host resources => increased costs

#### Agentless HIDS
* Information collected by streaming data over network
* (Pay for resources anyway? Just added network delay)
* (Added bonus of being able to compare data sources from multiple running containers of the same process? Easy anomaly detection via majority voting-esque thing?)

### Components
Normally has three core components

* **Data Collectors**: Sensors that collect and feed back data from hosts
* **Data Storage**: Data is aggregated and stored. Keep or don't (depending on budget) (might be useful to have on hand for later)
* **Analytics Engine**: Detect patterns/anomalies then assess likelihood that they are the result of security risks/attacks

### Common Detection Methods
#### Anomaly based
* Looks for unusual or irregular activity caused by users/processes
* E.g. login from multiple locations within the same day from same credentials
* Effective against attacks that don't have a signature
* Higher false positive rate than signature based

#### Signature-based
* Like sig-based detection in AVs: look for keywords/bit patterns in log files
* Good at identifying **known threats**
* Efficient processing (esp. compared to anomaly based)

---
## Questions for Ning

1. PC/Java listed in requirements. Any reason in particular?
2. How should I go about scoping of the project be. Just alert? Generate a report? Constant monitoring via dashboard?
3. What kind of systems knowledge should I focus on. I am comfortable with basic linux principles but could do with learning more for sure?
4. Is this a new project or have others done it before?
5. Building the analytics engine: question of pick some papers and implement them?
6. What would be needed for a good mark?
7. How is the system verified? I need to prove that certain threats are detected?
8. Will there be a novel research component or just an implementation?
	9.  if so, What significant challenges are there facing HIDS are there that I could look into
10. Legal/ethical considerations to be aware of?
11. Does UoM have datasets that I can look at/use to help implement signature-based detection?

---

## References

* https://sysdig.com/learn-cloud-native/detection-and-response/what-is-hids/
* https://www.dnsstuff.com/host-based-intrusion-detection-systems
* https://www.n-able.com/blog/intrusion-detection-system