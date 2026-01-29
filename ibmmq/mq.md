```sh
kubectl apply -f mq-simple.yaml 
pod/ibmmq-simple created


kubectl get po -n middleware
NAME           READY   STATUS    RESTARTS   AGE
ibmmq-simple   1/1     Running   0          69s
administrator@chnsdiubuntu02:~/middleware$ kubectl get po -A


kubectl get po -A -o wide

kubectl get po -n middleware -o wide
NAME           READY   STATUS    RESTARTS   AGE     IP           NODE             NOMINATED NODE   READINESS GATES
ibmmq-simple   1/1     Running   0          3m20s   10.0.0.254   chnsdiubuntu01   <none>           <none>

kubectl -n middleware exec -it ibmmq-simple -c ibmmq -- bash 

bash-5.1$ dspmqver
Name:        IBM MQ
Version:     9.4.4.1
Level:       p944-001-251203
BuildType:   IKAP - (Production)
Platform:    IBM MQ for Linux (x86-64 platform)
Mode:        64-bit
O/S:         Linux 6.8.0-86-generic
O/S Details: Red Hat Enterprise Linux 9.7 (Plow)
InstName:    Installation1
InstDesc:    IBM MQ V9.4.4.1 (Unzipped)
Primary:     N/A
InstPath:    /opt/mqm
DataPath:    /mnt/mqm/data
MaxCmdLevel: 944
LicenseType: Developer
ReleaseType: Continuous Delivery (CD)
```
```sh
qmgr related
ls /opt/mqm/bin
addmqinf    amqmfsck  amqspdbg	 amqzmuf0  dmpmqlog   dspmqrte	endmqtrc     mqrc	 runmqdlq    runswchl	  strmqbrk
amqcgskv64  amqoamd   amqsstop	 amqzmur0  dmpmqmsg   dspmqspl	endmqweb     rcdmqimg	 runmqicred  security	  strmqcsv
amqcrsta    amqorxr   amqwlpver  amqzxma0  dspmq      dspmqtrc	ffstsummary  rcrmqobj	 runmqktool  setmqaut	  strmqm
amqfcxba    amqp.sh   amqxdbg	 crtmqdir  dspmqaut   dspmqtrn	isa.xml      rmvmqinf	 runmqlsr    setmqenv	  strmqtrc
amqfqpub    amqpcsea  amqzfuma	 crtmqenv  dspmqcert  dspmqver	migmqlog     rsvmqtrn	 runmqras    setmqinst	  strmqweb
amqicdir    amqrcmla  amqzlaa0	 crtmqm    dspmqcsv   dspmqweb	mqcertck     runamscred  runmqsc     setmqm	  vermqpkg
amqiclen    amqrdbgm  amqzlsa0	 dltmqbrk  dspmqfls   endmqbrk	mqconfig     runmqakm	 runmqtmc    setmqprd
amqjrever   amqrfdm   amqzlwa0	 dltmqm    dspmqinf   endmqcsv	mqinstconf   runmqbrk	 runmqtrm    setmqspl
amqldmpa    amqrmppa  amqzmgr0	 dmpmqaut  dspmqinst  endmqlsr	mqlicense    runmqchi	 runp11cred  setmqweb
amqlrepa    amqrrmfa  amqzmuc0	 dmpmqcfg  dspmqlic   endmqm	mqperfck     runmqchl	 runqmcred   setmqxacred


client->qmgr related
ls /opt/mqm/samp
amqmdefs.tst  amqsauth.h    amqsecha.c	amqsiqma.c  amqspuba.c	amqsstma.c     amqstxvx.v	dlq		    pcf
amqsact0.c    amqsaxe0.c    amqsevta.c	amqslog0.c  amqsput0.c	amqsstop.c     amqsvfc0.c	jms		    preconnexit
amqsaem0.c    amqsbcg0.c    amqsfhac.c	amqsmhac.c  amqsqrma.c	amqssuba.c     amqswlm0.c	jms3.0		    pubsub
amqsaicq.c    amqsblst.c    amqsgbr0.c	amqsmon0.c  amqsreq0.c	amqstrg0.c     amqsxrma.c	mqat.ini	    service.env
amqsaiem.c    amqscbf0.c    amqsget0.c	amqsphac.c  amqsruaa.c	amqstxgx.c     bin		mqccred		    ubbstxcx.cfg
amqsailq.c    amqsclma.c    amqsghac.c	amqsprma.c  amqssbxa.c	amqstxpx.c     ccsid.new	mqclient.ini	    web
amqsapt0.c    amqscnxc.c    amqsgrma.c	amqspse0.c  amqsseta.c	amqstxsx.c     ccsid.tbl	mqmonitor.py	    wmqjava
amqsauth.c    amqscos0.tst  amqsinqa.c	amqsptl0.c  amqssslc.c	amqstxvx.flds  ccsid_part2.tbl	mqmonitor@.service  xatm

object related
ls /opt/mqm/samp/bin
amqauthg.sh  amqsaxe	amqscbfc  amqsevt   amqsghac  amqsiqmc	amqsppc   amqsptlc  amqsreqc  amqsset	amqsstmc
amqsact      amqsaxe_r	amqsclm   amqsfhac  amqsgr2   amqslog	amqspr1   amqspub   amqsres   amqssetc	amqssub
amqsactc     amqsbcg	amqscnxc  amqsgam   amqsgrm   amqslogc	amqspr2   amqspubc  amqsrr2   amqsspc	amqssubc
amqsaem      amqsbcgc	amqsdlq   amqsgbr   amqsgrmc  amqsmhac	amqsprm   amqsput   amqsrua   amqssr1	amqstrg
amqsaem_r    amqsblst	amqsdlqc  amqsgbrc  amqsinq   amqsmon	amqsprmc  amqsputc  amqsruac  amqssr2	amqstrgc
amqsapt      amqsblstc	amqsech   amqsget   amqsinqc  amqsmonc	amqspse   amqsqrm   amqssbx   amqssslc	amqswlm
amqsaptc     amqscbf	amqsechc  amqsgetc  amqsiqm   amqsphac	amqsptl   amqsreq   amqssbxc  amqsstm	amqsxrm
```
```
docker login http://172.27.8.7:8080
Username: admin
Password: 

#docker tag SOURCE_IMAGE[:TAG] 172.27.8.7:8080/middleware/REPOSITORY[:TAG]
docker build -t 172.27.8.7:8080/middleware/mq:v290126 -f Containerfile .
```


#docker push 172.27.8.7:8080/middleware/REPOSITORY[:TAG]
docker push 172.27.8.7:8080/middleware/mq:v290126
