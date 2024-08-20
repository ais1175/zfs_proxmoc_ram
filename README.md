ขนาดสูงสุดของ ZFS ARC
เมื่อไม่นานนี้ ฉันอ่านเจอข้อสับสนมากมายเกี่ยวกับ ZFS ที่ใช้ RAM เป็นจำนวนมาก

วิธีแก้ปัญหานั้นง่ายมาก เพียงแค่สร้างไฟล์การกำหนดค่าโมดูล zfs และตั้งค่าหน่วยความจำตามจำนวนที่ต้องการตามกฎ (4G + "จำนวน TB ทั้งหมดในพูล" * 1GB)

ทั้งหมดนี้อาจสร้างความสับสนได้มาก และถือเป็นการดำเนินการแบบครั้งเดียว ซึ่งต้องอ่านข้อมูลจำนวนมากเพื่อให้ตั้งค่าได้อย่างถูกต้อง

เพื่อลดความซับซ้อน ฉันจึงเขียนสคริปต์ที่ทำทุกอย่างด้วยตัวเอง และอนุญาตให้กำหนดขนาดด้วยตนเองหรือตั้งขนาดที่แนะนำโดยอัตโนมัติ

การกำหนดค่า
สคริปต์ค่อนข้างจะพร้อมใช้งานแล้ว แต่หากคุณต้องการตั้งค่าzfs.confตำแหน่งหรือชื่ออื่น โปรดแก้ไขmod_configตัวแปร

หากการติดตั้งของคุณมีโฟลเดอร์ pve อื่นที่ไม่ใช่/etc/pve(ซึ่งไม่น่าจะเป็นไปได้) ให้แก้ไขpve_dirตัวแปร

การใช้งาน
ดาวน์โหลด
รันในฐานะ root (เพราะว่า /etc/modprobe.d เป็นของ root และ config ต้องไปที่นั่น)
คำอธิบายสักเล็กน้อย
evaluated cache size- ที่แสดงโดยสคริปต์คือข้อมูลที่ประเมินด้วยผลรวมของขนาดพูลที่มีอยู่ในระบบโดยใช้สูตรด้านบน

recommended cache size- พิจารณาว่าevaluated cache sizeน้อยกว่า 8GB ขั้นต่ำที่แนะนำหรือไม่ กล่าวอีกนัยหนึ่ง: หากevaluated cache sizeน้อยกว่า 8GB ระบบจะแนะนำให้ตั้งค่าเป็น 8GB ในกรณีอื่น ระบบจะแนะนำให้ตั้งค่าเป็นค่าที่ประเมินแล้ว

ความคิดเห็นเกี่ยวกับคุณลักษณะ
เพิ่มความสามารถในการลบค่าจาก zfs.conf
