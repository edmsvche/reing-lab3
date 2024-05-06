<dependencies>
    <!-- JUnit 5 -->
    <dependency>
        <groupId>org.junit.jupiter</groupId>
        <artifactId>junit-jupiter-api</artifactId>
        <version>5.7.0</version>
        <scope>test</scope>
    </dependency>
    <dependency>
        <groupId>org.junit.jupiter</groupId>
        <artifactId>junit-jupiter-engine</artifactId>
        <version>5.7.0</version>
        <scope>test</scope>
    </dependency>
    <!-- Mockito -->
    <dependency>
        <groupId>org.mockito</groupId>
        <artifactId>mockito-core</artifactId>
        <version>3.6.0</version>
        <scope>test</scope>
    </dependency>
</dependencies>


package edu.pro;

import static org.junit.jupiter.api.Assertions.*;
import static org.mockito.Mockito.*;

import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.util.Map;

import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;

public class MainTest {

    private Path mockPath;

    @BeforeEach
    void setUp() {
        mockPath = mock(Path.class);
    }

    @Test
    void testReadAndCleanText() throws IOException {
        // Setup
        String expectedContent = "hello world";
        when(Files.readAllBytes(mockPath)).thenReturn("Hello1, World2!!!".getBytes());
        
        // Execute
        String actualContent = Main.readAndCleanText(mockPath.toString());

        // Verify
        assertEquals(expectedContent, actualContent.replaceAll("[^a-z ]", "").toLowerCase());
    }

    @Test
    void testCalculateFrequency() {
        String sampleText = "hello world hello";
        Map<String, Integer> frequency = Main.calculateFrequency(sampleText);

        assertEquals(2, frequency.get("hello"));
        assertEquals(1, frequency.get("world"));
    }

    @Test
    void testSortFrequencies() {
        Map<String, Integer> frequency = Map.of(
            "hello", 2,
            "world", 3,
            "test", 1
        );

        var sortedFrequencies = Main.sortFrequencies(frequency);
        assertEquals("world", sortedFrequencies.get(0).getKey());
        assertEquals(3, sortedFrequencies.get(0).getValue());
    }
}

package edu.pro;

import static org.junit.jupiter.api.Assertions.*;
import static org.mockito.Mockito.*;

import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.util.Collections;
import java.util.Map;

import org.junit.jupiter.api.Test;

public class MainTest {

    @Test
    void testReadAndCleanTextWithEmptyFile() throws IOException {
        Path path = mock(Path.class);
        when(Files.readAllBytes(path)).thenReturn(new byte[0]);

        String content = Main.readAndCleanText(path.toString());
        assertTrue(content.isEmpty());
    }

    @Test
    void testReadAndCleanTextWithOneWord() throws IOException {
        Path path = mock(Path.class);
        when(Files.readAllBytes(path)).thenReturn("Hello123".getBytes());

        String content = Main.readAndCleanText(path.toString());
        assertEquals("hello", content);
    }

    @Test
    void testHandlingLargeFile() throws IOException {
        Path path = mock(Path.class);
        byte[] largeData = new byte[1024 * 1024 * 50]; // Симуляція файлу розміром 50MB
        Arrays.fill(largeData, (byte) 'a');
        when(Files.readAllBytes(path)).thenReturn(largeData);

        String content = Main.readAndCleanText(path.toString());
        assertNotNull(content);
        assertFalse(content.isEmpty());
    }

    @Test
    void testIOExceptionHandling() {
        Path path = mock(Path.class);
        try {
            when(Files.readAllBytes(path)).thenThrow(new IOException("Failed to read"));

            Main.readAndCleanText(path.toString());
            fail("IOException expected but not thrown");
        } catch (IOException e) {
            assertEquals("Failed to read", e.getMessage());
        }
    }
}
import static org.junit.jupiter.api.Assertions.*;
import org.junit.jupiter.api.Test;

public class YourProjectTests {

    @Test
    public void testFile1Functionality() {
        // Тест для перевірки функціональності файлу 1
        // Реалізуйте тестовий випадок тут
    }

    @Test
    public void testFile2Functionality() {
        // Тест для перевірки функціональності файлу 2
        // Реалізуйте тестовий випадок тут
    }

    // Додайте інші тести для інших файлів за аналогією з вищенаведеними прикладами
}
#   r e i n g - l a b 3  
 