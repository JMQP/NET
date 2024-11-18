Stack Number	11	

Username    JOQU-007-M	  (student) 

Password	    2sTmj3FfSIha0wLJhtbE     

Red_NET    10.50.29.22
            	
Ping Sweep 


            for i in {1..254}; do (ping -c 1 192.168.65.$i | grep "bytes from" &) ; done
