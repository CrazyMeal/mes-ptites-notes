#stream 

# Enregistrement avec OBS
Paramétrage à faire:
1. Fichiers
2. Paramètres
3. Sortie
4. Onglet enregistrement
5. Mode de sortie: Avancé
6. Type: Personnalisé (FFmpeg)
7. Format du conteneur: mov
8. Encodeur vidéo: png
![[Pasted image 20221223161113.png]]

# Utilisation et re-export dans Davinci
Sur le clip importé:
1. Clic droit
2. Clip attributes
3. Alpha mode: Premultiplied
4. Jouer si besoin avec Field dominance

Paramétrage d'export:
1. Cocher Individual clips
2. Format: Quicktime
3. Codec: GoPro Cineform
4. Type: RGB 16-bit
5. Cocher Export Alpha
6. Alpha mode: Straight
7. Quality: Least
8. Data levels: full
![[Pasted image 20221223161442.png]]

# Utilisation dans OBS
1. Ajouter la source media
2. Pointer vers le fichier
3. Ne pas cocher accélération mériel, les RTX 20xx ne supportent pas les codec avec Alpha (cf [# NVIDIA Video Codec SDK](https://developer.nvidia.com/nvidia-video-codec-sdk) et la section pour le décodage vidéos et formats supportés)

# Lien utiles

[Export Transparency (Alpha Channel) in DaVinci Resolve!](https://www.youtube.com/watch?v=abPpcczGliE)