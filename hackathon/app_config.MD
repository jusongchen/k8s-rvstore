It communicates with other services:
• Auth service at: http://rvstore-auth-api:9003/auth
• Product service at: http://rvstore-product-api:9001/products
• Order service at: http://rvstore-order-api:9002/orders

• Order service at: http://rvstore-order-api:9002/orders

rvstore-order-api:9002



          env:
            - name: SPRING_PROFILES_ACTIVE
              value: compose


## Mongo DB 
          env:
            - name: MONGO_INITDB_ROOT_USERNAME
              value: mongoadmin
            - name: MONGO_INITDB_ROOT_PASSWORD
              value: secret



        volumeClaimTemplates:
          - metadata:
              name: {{ .Values.dataDisk.name }}
              labels:
                app: {{ .Values.kite.serviceIdentity }}
                component: {{ .Values.kite.serviceIdentity }}
            spec:
              accessModes: [ "ReadWriteOnce" ]
              resources:
                requests:
                  storage: {{ .Values.dataDisk.size }}
              storageClassName: {{ .Values.dataDisk.storageClass }}

## simulator
It communicates with the Gateway service at: http://rvstore-api-gateway:9000
• Only one copy of the application should run.
• Docker image: vergeops/k8s-rvstore-order-simulator
• Environment variables needed:
• SPRING_PROFILES_ACTIVE: compose