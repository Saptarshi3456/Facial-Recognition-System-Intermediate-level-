# Facial-Recognition-System-Intermediate-level-
Develop a facial recognition system.

import cv2
import face_recognition

# Load the image
image = cv2.imread('image.jpg')

# Detect faces
faces = face_recognition.face_locations(image)

# Extract face encodings
encodings = face_recognition.face_encodings(image, faces)

# Load the database of known faces
known_faces = []
known_names = []
for file in os.listdir('database'):
    image = cv2.imread('database/' + file)
    encoding = face_recognition.face_encodings(image)[0]
    known_faces.append(encoding)
    known_names.append(file.split('.')[0])

# Compare faces
for face, encoding in zip(faces, encodings):
    matches = face_recognition.compare_faces(known_faces, encoding)
    name = "Unknown"
    if True in matches:
        index = matches.index(True)
        name = known_names[index]
    cv2.rectangle(image, (face[3], face[0]), (face[1], face[2]), (0, 255, 0), 2)
    cv2.putText(image, name, (face[3], face[0] - 10), cv2.FONT_HERSHEY_SIMPLEX, 0.5, (0, 255, 0), 2)

# Display the output
cv2.imshow('Image', image)
cv2.waitKey(0)
cv2.destroyAllWindows()
