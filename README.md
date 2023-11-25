# Simple_Dictionary.py
เป็นการเขียนโปรแกรม Dictionary อย่างง่ายผ่านโปรแกรม PyCharm ด้วยภาษา Python 
โดยมี concept และเลือกใช้โครงสร้างข้อมูลชนิด Doubly Linked List ในการเขียน เนื่องจากสามารถค้นหาข้อมูลได้ทั้ง 2 ทิศทาง ( Next, Prev )
และมีการเพิ่งคำสั่ง เพิ่ม ลบ และค้นหา คำศัพท์เข้าไปด้วย หรือที่เรียกว่า (CRUD operations)

Doubly Linked List คืออะไร
    เป็นโครงสร้างของข้อมูล ที่เก็บข้อมูลไว้ใน node เป็นลำดับ โดยแต่ละ node จะประกอบไปด้วยข้อมูลและ pointer 2ตัว ชี้ไปยังnode ถัดไป (Next) และอีกหนึ่งตัวชี้ไปยัง node ก่อนหน้า (Prev) ยกเว้น node แรกที่ Pointer สำหรับชี้ไป node ก่อนหน้าจะชี้ไปที่ null และnode สุดท้ายที่ pointer สำหรับชี้ไป node ถัดไปจะชี้ไปที่ null ถ้านํา node มาเรียงต่อๆกัน เป็นลำดับจะได้ doubly linked list ของข้อมูล n ตัวโดยจะกำหนดให้มี pointer อย่างน้อย1ตัวที่ชี้ไปยัง node ตัวแรกของ doubly linkedlist เสมอ

![image](https://github.com/twbengutcc/Simple_Dictionary.py/assets/150536808/d0d1bc71-7d56-4e3a-b709-91d0aa06e52a)


ตัวอย่างการใช้งาน ** ( Next, Prev )**  Code ( Next, Prev ) ในส่วนของ class

    def get_next(self):
        if self.current_node and self.current_node.next:
            self.current_node = self.current_node.next
            return f"{self.current_node.english} ({self.current_node.word_type}): {self.current_node.thai}"
        else:
            return "ไม่มีข้อมูลถัดไป"

    def get_previous(self):
        if self.current_node and self.current_node.prev:
            self.current_node = self.current_node.prev
            return f"{self.current_node.english} ({self.current_node.word_type}): {self.current_node.thai}"
        else:
            return "ไม่มีข้อมูลก่อนหน้า"

![image](https://github.com/twbengutcc/Simple_Dictionary.py/assets/150536808/efa6616b-e5e2-48ff-afb2-117db5f93bd6)

![image](https://github.com/twbengutcc/Simple_Dictionary.py/assets/150536808/62c0bf9a-3925-4220-b7f0-c28abda8acfb)


ตัวอย่างการใช้งานการค้นหาคำศัพท์ code Search ในส่วนของ class
    
    def search(self, english):
        current = self.head
        while current:
            if current.english == english:
                return current
            current = current.next
        return None
        
![image](https://github.com/twbengutcc/Simple_Dictionary.py/assets/150536808/7adee4ad-588e-4254-8eae-2a13149ce2fe)

ตัวอย่างการใช้งานการเพิ่มคำศัพท์ code Add Word ในส่วนของ class

      def add_word(self, english, thai, word_type):
        new_node = Node(english, thai, word_type)
        if not self.head:
            self.head = new_node
            self.tail = new_node
            self.current_node = new_node
        else:
            new_node.prev = self.tail
            self.tail.next = new_node
            self.tail = new_node

        self.sort_words()

![image](https://github.com/twbengutcc/Simple_Dictionary.py/assets/150536808/fb54c9d8-a2e4-4615-949f-3b8f099e4dfb)

![image](https://github.com/twbengutcc/Simple_Dictionary.py/assets/150536808/79893855-d07b-4bf6-8de2-7a79d739c966)


ตัวอย่างการใช้งานการลบคำศัพท์ code Delete Word ในส่วนของ class

    def delete_word(self, english):
        current = self.head
        while current:
            if current.english == english:
                if current.prev:
                    current.prev.next = current.next
                else:
                    self.head = current.next

                if current.next:
                    current.next.prev = current.prev
                else:
                    self.tail = current.prev

                if current == self.current_node:
                    self.current_node = current.next

                self.sort_words()
                return True
            current = current.next
        return False

![image](https://github.com/twbengutcc/Simple_Dictionary.py/assets/150536808/c00797d4-6cb5-4607-a081-03240bf71771)

![image](https://github.com/twbengutcc/Simple_Dictionary.py/assets/150536808/f607dcb1-94e6-480a-919e-c7890a44323e)
