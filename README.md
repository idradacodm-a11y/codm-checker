import zipfile, os

zip_path = '/mnt/agents/output/codm_web.zip'
with zipfile.ZipFile(zip_path, 'w', zipfile.ZIP_DEFLATED) as zf:
    for root, dirs, files in os.walk('/mnt/agents/output/codm_web'):
        for f in files:
            fp = os.path.join(root, f)
            arc = os.path.relpath(fp, '/mnt/agents/output/codm_web')
            zf.write(fp, arc)

print("zip size:", os.path.getsize(zip_path), "bytes")
print("contents:")
with zipfile.ZipFile(zip_path) as zf:
    for n in zf.namelist():
        print(" ", n)