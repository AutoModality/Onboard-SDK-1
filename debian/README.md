# Packaging Onboard-SDK-4.0

* The goal is to make as few custom changes to this repository as possible. 
* Consider making custom changes to one of our repos that extends this library.
* We forked this repository so we could provide debian binary packages for easy and consistent distributions.

Changes are currently found under two directories introduced by AM:

* debian/
* .github/

Let's keep it that way.


## Github Actions

.github/workflows contains custom workflows catering to an external development lifecycle. 

* Story branches remain the same and will produce release candidates in Cloudsmith
* Release branches require manual input of version by modifying the `.github/workflows/release.yml`
    * Use their most recent [release tag](https://github.com/AutoModality/Onboard-SDK-4.0/releases) as the base
    * Append `-AM##` replacing `#` with incrementing two digit number with leading zeros: `4.0.0-AM01`, `4.0.0-AM02`
    * Failure to increment this value will result in failed deployment to Cloudsmith

### ARM 64 Builder

We provide self hosted runners to build our ARM binaries, however, this can cause a [security threat](https://help.github.com/en/actions/hosting-your-own-runners/about-self-hosted-runners#self-hosted-runner-security-with-public-repositories).  
For this reason, we only bring up the self hosted runner manually when builds need to happen, which should be rare.

1. `ssh nvidia@192.168.4.135`
1. `/media/nvidia/build/actions-runners/Onboard-SDK-4.0/run.sh`
1. You should see `√ Connected to GitHub` and `Listening for Jobs`
1. You should see `arm-builder` available in the [repo's actions](https://github.com/AutoModality/Onboard-SDK-4.0/settings/actions)
