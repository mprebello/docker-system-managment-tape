
# Download this content
  -> git clone https://github.com/mprebello/docker-system-managment-tape

# Edit docker-system-managment-tape/code/tapesystem/conf/BackEnd/config.json
  -> Fill with database connection

# Edit docker-system-managment-tape/code/tapesystem/Dockerfile
  -> edit proxy information

#compile docker
  ->  # cd docker-system-managment-tape/code
  ->  # docker-compose build

#everything ok up the server
  -> # docker-compose up -d
