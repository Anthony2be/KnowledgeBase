# How to Extract Minecraft Sounds (python required):
make a .py file and inside put:
```Python
import json, os, platform, shutil, sys
print("Your OS is " + platform.system())
if platform.system() == "Windows":
    MC_ASSETS = os.path.expandvars(r"%APPDATA%/.minecraft/assets")
else:
    MC_ASSETS = os.path.expanduser(r"~/.minecraft/assets")

MC_VERSION = os.listdir(MC_ASSETS+"/indexes/")[-1]
MC_VERSION = input("what version do you want to extract (ex 1.16 or 1.8)? ")
print("The version of minecraft that is getting extracted is " + MC_VERSION + "\n")
MC_VERSION += ".json"


OUTPUT_PATH = os.path.normpath(os.path.expandvars(os.path.expanduser(f"~/Desktop/MC_Sounds/")))


MC_OBJECT_INDEX = f"{MC_ASSETS}/indexes/{MC_VERSION}"
MC_OBJECTS_PATH = f"{MC_ASSETS}/objects"
MC_SOUNDS = r"minecraft/sounds/"


with open(MC_OBJECT_INDEX, "r") as read_file:
    data = json.load(read_file)
    sounds = {k[len(MC_SOUNDS):] : v["hash"] for (k, v) in data["objects"].items() if k.startswith(MC_SOUNDS)}

    print("File extraction :")

    for fpath, fhash in sounds.items():
        src_fpath = os.path.normpath(f"{MC_OBJECTS_PATH}/{fhash[:2]}/{fhash}")
        dest_fpath = os.path.normpath(f"{OUTPUT_PATH}/sounds/{fpath}")
        print(fpath)
        os.makedirs(os.path.dirname(dest_fpath), exist_ok=True)
        shutil.copyfile(src_fpath, dest_fpath)
```
Then save and run it. If you did it correctly there should be a new folder on your desktop containing the files

(Copy and Paste Extract from Knowledge Base <https://discord.gg/xpNJdH9>)
(Discord Raw Paste, Github paste, and Example Pack <https://github.com/SheepCommander/KnowledgeBase/tree/main/faq/how-to-extract-sounds>)
