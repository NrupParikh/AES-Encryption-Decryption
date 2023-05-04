# AES-Encryption-Decryption
Sample code for implementing AES Encryption and Decryption

```kotlin
import android.util.Base64
import java.security.Key
import javax.crypto.Cipher
import javax.crypto.spec.SecretKeySpec


object AESCrypt {
    private const val ALGORITHM = "AES"
    private const val KEY = "5GJfh607edfBEJ62"

    @JvmStatic
    fun encrypt(value: String): String? {
        val key: Key = generateKey()
        val cipher: Cipher = Cipher.getInstance(ALGORITHM)
        cipher.init(Cipher.ENCRYPT_MODE, key)
        val encryptedByteValue: ByteArray =
            cipher.doFinal(value.toByteArray(charset("utf-8")))
        return Base64.encodeToString(encryptedByteValue, Base64.DEFAULT).trim()
    }

    @JvmStatic
    fun decrypt(value: String?): String? {
        if (value.isNullOrEmpty()) return ""
        return try {
            val key: Key = generateKey()
            val cipher: Cipher = Cipher.getInstance(ALGORITHM)
            cipher.init(Cipher.DECRYPT_MODE, key)
            val decryptedValue64: ByteArray = Base64.decode(value, Base64.DEFAULT)
            val decryptedByteValue: ByteArray = cipher.doFinal(decryptedValue64)
            String(decryptedByteValue, charset("utf-8"))
        } catch (e: Exception) {
            ""
        }
    }

    private fun generateKey(): Key {
        return SecretKeySpec(KEY.toByteArray(), ALGORITHM)
    }
}

// Usage 

AESCrypt.encrypt(password).toString()
AESCrypt.decrypt(it.Password)

```
