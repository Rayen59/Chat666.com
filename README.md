  
import React, { useEffect, useRef } from 'react';
  
// Example Avatar component
const Avatar = ({ size, name, src }) => (
    <img 
        src={src} 
        alt={name} 
        style={{ width: size === 'sm' ? '40px' : '80px', height: 'auto', borderRadius: '50%' }} 
    />
);

const CreateUserProfile = () => {
    const textareaRef = useRef(null);

    const handleInput = () => {
        if (textareaRef.current) {
            textareaRef.current.style.height = 'auto'; // Reset the height
            textareaRef.current.style.height = `${textareaRef.current.scrollHeight}px`; // Set height based on content
        }
    };

    useEffect(() => {
        handleInput(); // Set initial height based on content when the component mounts
    }, []);

    return (
        <div className='createuserProfile'>
            <div className='fig'>
                <Avatar size='sm' name='Kent Dodds' src='https://bit.ly/kent-c-dodds' />
            </div>
            <textarea 
                ref={textareaRef} 
                placeholder='What’s up ?' 
                onInput={handleInput}
                style={{ backgroundColor: 'red', width: '300px', minHeight: '40px', resize: 'none', overflow: 'hidden' }}
            />
        </div>
    );
};

export default CreateUserProfile;


const [fileName, setFileName] = useState('');
const [image,setImage] = useState('')
 

 


const handleFileChange = async (e) => {
  const file = e.target.files[0];
  setFileName(file.name); // Update state with the selected image
 
  // Ensure an image is selected
  if (!fileName) return;

  const formData = new FormData();
  formData.append("file", fileName);
  formData.append("upload_preset", 'ask-app'); // Replace with your Cloudinary upload preset
 
  try {
    // Upload the image to Cloudinary
    const uploadResponse = await axios.post(
      'https://api.cloudinary.com/v1_1/dfmdgsiid/upload', // Replace with your Cloudinary cloud name
      formData
    );
    console.log(uploadResponse.data.secure_url); 
    setImage(uploadResponse.data.secure_url)
    
  } catch (error) {
    console.log(`This error is caused by ${error}`); // Corrected typo in "error"
    setLoading(false)
  }
};


