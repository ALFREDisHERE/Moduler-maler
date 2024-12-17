# Terraform Azure Load Balancer Konfigurasjon

Denne Terraform-konfigurasjonen oppretter en Azure Load Balancer med en HTTP-probe og en regel for TCP-trafikk på port 3306. Oppsettet inkluderer også en backend-adressepool for å administrere tilkoblede servere.

## Krav

- **Terraform** installert på maskinen.
- En eksisterende Azure-ressursgruppe.
- Et eksisterende subnett i et virtuelt nettverk.

## Konfigurasjon

### Variabler

Definerte variabler i `terraform.tfvars`:

- `location`: Azure-regionen der ressursene skal opprettes (f.eks., "West Europe").
- `resource_group_name`: Navnet på Azure-ressursgruppen der ressursene skal opprettes.
- `subnet_id`: ID-en til subnettet der Load Balancerens frontend-IP-konfigurasjon skal knyttes.

### Brukerveiledning

1. Klon dette repositoriet og naviger til prosjektmappen.
2. Tilpass `terraform.tfvars` basert på dine behov.
3. Initialiser Terraform:

    ```bash
    terraform init
    ```

4. Forhåndsvis infrastrukturen som skal opprettes:

    ```bash
    terraform plan
    ```

5. Implementer konfigurasjonen:

    ```bash
    terraform apply
    ```

### Utdataverdier

- `lb_id`: ID-en til den opprettede Load Balanceren.

### Opprettede ressurser

- **Azure Load Balancer**: Konfigurert med standard SKU og støtte for TCP-protokoll på port 3306.
- **Backend-adressepool**: En pool som administrerer backend-serverne for lastbalansering.
- **Health Probe**: En HTTP-probe konfigurert for å overvåke tilkoblinger på TCP-port 3306.
- **Load Balancer-regel**: Ruting av TCP-trafikk fra frontend til backend på port 3306.

## Merknader

Denne konfigurasjonen forutsetter at både subnettet og ressursgruppen allerede eksisterer. Juster `main.tf` dersom oppsettet krever tilpasninger.
