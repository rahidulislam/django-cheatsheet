  
# Wand -> how to create image images from pdf's and save it to database
  
  
    path = os.path.join(settings.BASE_DIR,"media/resume/",file_name)
    pdf = wi(filename=path, resolution=300)
    image = pdf.convert("jpeg")
    print(image)
    i=1
    resume_obj.resume_image.set([])
    for img in image.sequence:
                
        print("yes")
        obj = models.ImagePdf.objects.create(resume_id=resume_obj)
        print("yes")
        fname = f"{obj.id}image.jpg"
        file_dir = os.path.join(settings.BASE_DIR,"media/imagepdf/", fname)
        print("yes")
        page = wi(image=img)
        print("yes")
        a = page.save(filename=file_dir)
        obj.pdf_image="https://dev.kalke.co/media-candidates/imagepdf/"+fname
        obj.image = "/imagepdf/"+fname
        obj.save()
        print("yes")
               
        resume_obj.resume_image.add(obj)
        resume_obj.save()
        i+=1
