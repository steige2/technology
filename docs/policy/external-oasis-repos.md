
Policy for OSG Mirroring of External CVMFS repositories
=====================================================
12 October 2017

This document provides an overview of the policies and security understanding with regards to OSG mirroring of CVMFS
repositories of external organizations.  It aims to help external repositories and OSG VOs understand what OSG is
attempting to achieve with the mirroring service.
This is not a service-level agreement but rather a statement of responsibilities.

!!! note:
    To actually understand the technical procedure for mirroring a repository, [see the following page](https://twiki.grid.iu.edu/bin/view/Documentation/Release3/OasisExternalRepositories).  This document solely covers the policy aspects.

Introduction
------------

The OSG provides a network of CVMFS Stratum-1 servers for mirroring content of externally-managed repositories.  These repositories are often
hosted by large HEP or physics VOs for the purpose of distributing software for high-throughput computing jobs.  Additionally, OSG provides a
repository (<oasis.opensciencegrid.org>) for smaller VOs; this is not covered here.

OSG will include additional repositories into the content distribution network (CDN) at the request of an OSG-affiliated VO.  These repositories
are meant to help the OSG-affiliated VO accomplish their domain science.

The goal of this mirroring provides an improved quality-of-service for the VO end-users running at OSG sites.  OSG does not provide support
for use of the software in external repositories, but will help end-users contact the VO for help as necessary.

OSG Responsibilities
---------------------

* OSG will provide the Stratum-1 server network according to [the OASIS SLA](https://opensciencegrid.github.io/operations/SLA/oasis-replica/)
* OSG will provide a best-effort mirror of the full contents of the external repo.  We will attempt to provide best-effort integrity of the
  object contents, but assume users of the Stratum-1 will do further integrity checking.  No SLA is provided covering potential data corruptions.
* OSG will provide best-effort notification to the mirrored repository in case OSG detects a service outage of the external repo.
* In the event of a reported security incident, OSG will replace the repository contents with an empty directory, signed by an OSG-managed key.
  This will be done under the direction of the security team.
* Once the external repository is approved, OSG will distribute the corresponding repository signing keys in a valid whitelist.  The whitelist
  will be signed by the OSG Stratum-0.  This whitelist attests to the authenticity of the key, but not a statement about repository contents.

VO Responsibilities
-------------------
* The individual responsible on behalf of the VO will be registered with the OASIS Manager role in OIM.
* The requesting VO should only include targeted repositories they need to support their science.
* The VO should understand that in the event of a reported security incident, the contents of this repository may be replaced with an
  empty directory and signed by the OSG repository key.  Depending on the OSG Security team's evaluation of the severity and urgency
  of the incident, the blanking may be done immediately without VO notification or after some notification period.
* In the case of a security incident, the VO and OSG Security team will need to mutually agree that the incident is resolved before the
  repository is unblanked.
* The VO is ultimately responsible for the contents of the repository.  OSG provides a mirror.
* If the external repository is *not* operated by the VO, OSG may work directly with the external repository maintainers.  This is done for
  ease of operations and may be limited to day-to-day, non-security-related support.

