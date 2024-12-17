# Terraform: Oppsett av Virtuelt Nettverk og Subnett i Azure

Denne Terraform-konfigurasjonen oppretter et virtuelt nettverk i Azure med to subnett (ett for webservere og ett for databaseservere) samt en nettverkssikkerhetsgruppe (NSG) som tillater HTTP-trafikk på port 80.

## Krav

- **Terraform** installert på systemet.
- En eksisterende Azure-ressursgruppe.

## Konfigurasjon

### Nødvendige Variabler

Disse variablene må spesifiseres i `terraform.tfvars`:

- `vnet_name`: Navnet på det virtuelle nettverket (f.eks., `"VNet-Prod"`).
- `location`: Azure-regionen der ressursene skal opprettes (f.eks., `"West Europe"`).
- `resource_group_name`: Navnet på ressursgruppen i Azure.
- `address_space`: Liste over adresseområder for det virtuelle nettverket (f.eks., `["10.0.0.0/16"]`).
- `web_subnet_name`: Navnet på subnettet for webservere.
- `web_subnet_prefix`: Adresseområde for webserver-subnettet (f.eks., `"10.0.1.0/24"`).
- `db_subnet_name`: Navnet på subnettet for databaseservere.
- `db_subnet_prefix`: Adresseområde for databaseserver-subnettet (f.eks., `"10.0.2.0/24"`).

### Bruksanvisning

1. **Klon prosjektet**:
   Last ned dette repositoriet og naviger til prosjektmappen.

2. **Tilpass variablene**:
   Rediger `terraform.tfvars` med dine spesifikke verdier:

    ```hcl
    vnet_name = "Navn på ditt virtuelle nettverk"  # Eks.: "VNet-Prod"
    location = "Azure-regionen din"  # Eks.: "West Europe"
    resource_group_name = "Navn på ressursgruppen din"
    address_space = ["10.0.0.0/16"]  # Tilpass adresseområdet for VNet
    web_subnet_name = "Navn på web-subnett"  # Eks.: "WebSubnet"
    web_subnet_prefix = "10.0.1.0/24"  # Tilpass adresseområdet for web-subnett
    db_subnet_name = "Navn på database-subnett"  # Eks.: "DbSubnet"
    db_subnet_prefix = "10.0.2.0/24"  # Tilpass adresseområdet for database-subnett
    ```

3. **Initialiser Terraform**:
   Start Terraform for å laste nødvendige moduler og plugins:

    ```bash
    terraform init
    ```

4. **Planlegg infrastrukturen**:
   Generer en oversikt over hvilke ressurser som vil bli opprettet:

    ```bash
    terraform plan
    ```

5. **Opprett ressursene**:
   Implementer infrastrukturen:

    ```bash
    terraform apply
    ```

### Utdataverdier

Etter at ressursene er opprettet, vil følgende verdier være tilgjengelige:

- `vnet_id`: ID-en til det opprettede virtuelle nettverket.
- `web_subnet_id`: ID-en til webserver-subnettet.
- `db_subnet_id`: ID-en til databaseserver-subnettet.

### Opprettede Ressurser

- **Virtuelt Nettverk**: Konfigurert med det spesifiserte adresseområdet.
- **Subnett**:
  - Webserver-subnett: For frontend- eller applikasjonstjenester.
  - Databaseserver-subnett: For backend-databasetjenester.
- **Nettverkssikkerhetsgruppe (NSG)**: Tillater innkommende HTTP-trafikk på port 80 til webserverne.

## Notater

- Denne konfigurasjonen krever en eksisterende ressursgruppe i Azure. 
- Du kan tilpasse konfigurasjonen ytterligere ved å redigere `main.tf` og variablene i `terraform.tfvars`.


