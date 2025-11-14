# T03: Gestió flexible de discos (Storage Spaces)

## Crear discos addicionals virtuals per al Storage Pool

<img width="175" height="175" alt="Unofficial_Windows_logo_variant_-_2002–2012_(Multicolored) svg" src="https://github.com/user-attachments/assets/9b21570a-326f-434d-9612-45de8fd51a3f" />

Obre la configuració de la VM.

A l’apartat Emmagatzematge (Storage), afegeix tres discos nous de 10 GB cadascun.

Desa i reinicia la VM.  
Que quedi així:  

<img width="752" height="429" alt="1" src="https://github.com/user-attachments/assets/c4b27b24-678e-4bc8-b8c3-04dd4683333e" />


**Hem de seleccionar els tres discos creats** 

<img width="753" height="61" alt="2" src="https://github.com/user-attachments/assets/e7286f46-8a41-4719-b063-cf3eac67b4b3" />


**RESILIENCIA DE MIRALL**

Seleccionem dos discos a \< **Administrar espacios de almacenamiento de discos** \>

<img width="606" height="342" alt="3" src="https://github.com/user-attachments/assets/9fafeadf-45df-437e-b52a-a7ad8f27439e" />


Un cop seleccionats aquests dos discos hem d'afegir el 

Tipos de resilencia**: Reflejo doble** 

**I en la mida màxima posem 20 GB** 

**Un cop assignats els dos discos eliminem un per comprovar que passaria si eliminem un.**

<img width="520" height="354" alt="4" src="https://github.com/user-attachments/assets/dcf013a1-acbd-44be-99f4-64009cee2166" />


**Creem un arxiu per veure que succeeix si esborrem un disc:** 

<img width="636" height="471" alt="5" src="https://github.com/user-attachments/assets/1b9fa5ad-7608-476c-897a-034589c8fb27" />

**Un cop eliminat ens donarà una advertència de què ha desaparegut un disc**

<img width="662" height="388" alt="6" src="https://github.com/user-attachments/assets/63cac9e3-6ab0-4d57-aab8-d7bcedddd8bd" />


**un cop eliminat un disc hem d'afegir un disc que agafi la mateixa referència que tenia el disc anterior.**

<img width="469" height="307" alt="7" src="https://github.com/user-attachments/assets/aad0192d-5eed-4603-952f-556f72a2d783" />


**Com podem veure seguim tenint els dos discos que teníem anteriorment i a més segueixen tenint la informació (en aquest cas arxiu) que tenia abans:**

<img width="457" height="418" alt="8" src="https://github.com/user-attachments/assets/01a5cda3-7602-42e5-a2cd-e7841b65a5c9" />


**I ara podrem esborrar la unitat de disc perquè no surti més la seva exportació:**

**Mirall triple**  
Desfer l’espai anterior i crear un amb els tres discos que sigui mirall triple. Justificar quins avantatges té respecte al mirroring.  
    
<img width="481" height="302" alt="9" src="https://github.com/user-attachments/assets/8c51430a-b6e7-4dc4-83d6-4e536474185d" />


**Després d'afegir 5 discos hem d'obrir la màquina virtual.**

**Seguidament hem d'obrir la gestió de discs i inicialitzar els discos:**

<img width="429" height="318" alt="10" src="https://github.com/user-attachments/assets/2fbac958-abc8-4d83-84c9-d00fae0f12ec" />


<img width="353" height="378" alt="11" src="https://github.com/user-attachments/assets/847eafd8-1eb8-4133-8952-6f46b43f165f" />



**Ara un cop afegit veurem la tolerancia a les fallades, hem eliminat 2 discos, amb la màquina virtual apagada, un cop hem eliminat aquests 2 discos hem d encedre la màquina i comprovar si la informació està encara.** 

<img width="448" height="480" alt="12" src="https://github.com/user-attachments/assets/101815cc-792c-4012-8be1-0cc3e611a3ac" />


**Com podem veure, no hi ha cap error, i un dels documents anteriorment creats apareixen  correctament.** 

<img width="349" height="390" alt="13" src="https://github.com/user-attachments/assets/f4afaba6-913d-45e1-a551-f16bab784969" />


**Com podem veure, ens surt advertència als discos que hem desactivat, un cop ens surt que estan desactivant hem d’activar-los un altre cop amb la màquina apagada**

<img width="555" height="92" alt="14" src="https://github.com/user-attachments/assets/1e1982d0-f41f-4da8-8d0e-edae83e7ead8" />


**Un cop hem activat els discos novament, també 		ens surten tots els arxius correctament** 

<img width="479" height="499" alt="16" src="https://github.com/user-attachments/assets/33440a43-2a5a-435e-872b-a26dea0c0b83" />

<img width="726" height="492" alt="º7" src="https://github.com/user-attachments/assets/8aa9e581-4403-4513-9bba-d3b4849c923f" />
