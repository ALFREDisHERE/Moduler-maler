# Terraform: Oppsett av Azure Virtual Machine

Denne Terraform-konfigurasjonen oppretter en Linux Virtual Machine (Debian 12) i Azure, med et nettverksgrensesnitt tilknyttet et spesifisert subnett.

## Krav

- **Terraform**: Må være installert på maskinen din.
- **Eksisterende ressursgruppe og subnett**: Ressursgruppen og subnettet i Azure må være opprettet på forhånd.

## Konfigurasjon

### Variabler

Definer følgende variabler i `terraform.tfvars`:

- `vm_name`: Navnet på den virtuelle maskinen (f.eks., `"ProdVM"`).
- `location`: Azure-regionen hvor VM-en skal opprettes (f.eks., `"West Europe"`).
- `resource_group_name`: Navnet på den eksisterende ressursgruppen i Azure.
- `subnet_id`: ID-en til subnettet der VM-en skal plasseres.
- `vm_size`: Størrelsen på VM-en. Standardverdi er `"Standard_B1s"`.
- `admin_username`: Brukernavn for administrasjonsbrukeren.
- `admin_password`: Passord for administrasjonsbrukeren. Sørg for at passordet er sterkt og oppfyller sikkerhetskravene.

### Brukerveiledning

1. **Klon prosjektet**:
   Last ned dette repositoriet og naviger til prosjektmappen.

2. **Opprett en variabelfil**:
   Lag en fil kalt `terraform.tfvars` og fyll den med verdier som passer dine behov. Eksempel:

    ```hcl
    vm_name = "ProdVM"
    location = "West Europe"
    resource_group_name = "MyResourceGroup"
    subnet_id = "/subscriptions/<subscription_id>/resourceGroups/<resource_group>/providers/Microsoft.Network/virtualNetworks/<vnet_name>/subnets/<subnet_name>"
    vm_size = "Standard_B1s"
    admin_username = "adminuser"
    admin_password = "SterktPassord123!"
    ```

3. **Initialiser Terraform**:
   Kjør følgende kommando for å laste nødvendige moduler og plugins:

    ```bash
    terraform init
    ```

4. **Planlegg distribusjonen**:
   Forhåndsvis hvilke ressurser som vil bli opprettet:

    ```bash
    terraform plan
    ```

5. **Opprett ressursene**:
   Utfør distribusjonen ved å bruke følgende kommando:

    ```bash
    terraform apply
    ```

### Utdataverdier

Etter vellykket distribusjon vil Terraform generere følgende utdata:

- `vm_id`: ID-en til den opprettede virtuelle maskinen.
- `public_ip_address`: Offentlig IP-adresse knyttet til VM-en.

### Opprettede Ressurser

- **Azure Network Interface (NIC)**: Nettverksgrensesnitt knyttet til det spesifiserte subnettet.
- **Azure Virtual Machine (Debian 12)**: En Debian 12-basert VM konfigurert med spesifisert størrelse, administrasjonsbrukernavn, og passord.

## Merknader

- Denne konfigurasjonen forutsetter at både ressursgruppen og subnettet allerede eksisterer. Om nødvendig kan `main.tf` justeres for å inkludere opprettelse av disse ressursene.
- Bruk alltid sterke passord og vurder å bruke SSH-nøkler i stedet for passord for økt sikkerhet.
