#### User interaction

```mermaid
      graph TD
          DS(Data Storage - DS)

          subgraph Infrastructure
          subgraph actinia-VM
          DS1(DS)
          manager(<b>actinia manager</b>)
          end
          subgraph keycloak-VM
          keycloak(<b>Keycloak</b>)
          postgres(Postgres)
          end
          subgraph redis-VM
          redis(<b>redis<br>job queue + resources</b>)
          end
          subgraph on-demand worker VM
          DS2(DS)
          worker(<b>actinia worker</b>)
          end
          end

          manager --> redis
          worker --> redis
          manager --> keycloak
          keycloak --> postgres
          %%DS -- mount --> DS1
          %%DS -- mount --> DS2
          %%DS1 -- mount --> manager
          %%DS2 -- mount --> worker

          classDef docker fill:#df65b0;
          class docker,manager,keycloak,postgres,redis docker;
          classDef charliecloud fill:#e9a3c9;
          class charliecloud,worker charliecloud;
          classDef ds fill:#a1d76a;
          class mount,DS,DS1,DS2 ds;
