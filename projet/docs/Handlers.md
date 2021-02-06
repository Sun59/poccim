# tasks file for apache
    - name: install apache2
      apt: name=apache2 update_cache=yes state=latest
      
    - name: "Create docuement root"
      file:
          path: "/var/www/{{ ap_http_host_dir }}"
          state: directory
     
    - name: "Copy source html"
      copy:
         src: "/Users/samirhammouti/Projet/projet/site"
         dest: "/var/www/{{ ap_http_host_dir }}"  
	
	